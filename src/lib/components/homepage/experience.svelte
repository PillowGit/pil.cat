<script lang="ts">
  import { onMount } from "svelte";
  import exp_dat from './experience.json';
  let debug: string = "";
  
  // Store all experience entries
  interface ExperienceEntry {
    start_yr: number;
    end_yr: number;
    name: string;
    title: string;
    date: string;
    desc: string;
    company: string;
  }
  const entries: ExperienceEntry[] = exp_dat["entries"] as ExperienceEntry[];
  let choice: number = entries.length - 1;

  // Gather a list of years to display
  const start_yr: number = 2021;
  let year_nums = Array.from({length: new Date().getFullYear() - start_yr + 1}, (_, i) => start_yr + i);

  // Store the elements for each year to render the timeline
  interface YearElement {
    year: number;
    dot: HTMLElement;
    text: HTMLElement;
  }
  interface YearElements {
    [year: number]: YearElement;
  }
  let years: YearElements = {};

  // Function to move the highlighted bit of the timeline to the selected years
  let old_line: HTMLElement | null = null;
  function centerOfDot(dot: HTMLElement): number[] {
    return [dot.offsetLeft + dot.offsetWidth / 2, dot.offsetTop + dot.offsetHeight / 2];
  }
  function renderTimeline() {
    if (old_line !== null) {
      old_line.remove();
    }
    for (let year in years) {
      years[year].dot.className = years[year].dot.className.replace(" active_dot", "");
    }
    const exp: ExperienceEntry = entries[choice];
    if (exp.start_yr === exp.end_yr) {
      years[exp.start_yr].dot.className += " active_dot";
    } else {
      for (let year = exp.start_yr; year <= exp.end_yr; year++) {
        years[year].dot.className += " active_dot";
      }
      const left_pos: number[] = centerOfDot(years[exp.start_yr].dot);
      const right_pos: number[] = centerOfDot(years[exp.end_yr].dot);
      const line: HTMLElement = document.createElement("div");
      years[exp.start_yr].dot.parentElement?.appendChild(line);
      const line_style: string = `position: absolute; top: ${left_pos[1]}px; left: ${left_pos[0]}px; width: ${right_pos[0] - left_pos[0]}px; height: 0.25vh; background-color: var(--font-color);`;
      line.setAttribute("style", line_style);
      old_line = line;
    }
    // Alert the dots coordinates
  }

  // Update debug to be the mouse position
  function updateDebugText(event: MouseEvent) {
    debug = `(${event.clientX}, ${event.clientY})`;
  }

  onMount(() => {
    for (let year of year_nums) {
      const dot: HTMLElement | null = document.getElementById(year+"-dot");
      const text: HTMLElement | null = document.getElementById(year+"-text");
      if (dot === null || text === null) {
        alert("Error: Couldn't find HTML elements on the timeline");
        return;
      }
      years[year] = {
        year: year,
        dot: dot,
        text: text
      };
    }
    document.addEventListener("mousemove", updateDebugText);
    document.addEventListener("resize", renderTimeline);
    renderTimeline();
  });

</script>

<div class="title-text timeline-title">Experience</div>
<div class="timeline-holder">
  <div class="years">
    {#each year_nums as year}
      <div class="year">
        <span class="xs-text year-text" id={year+"-text"}>{year}</span>
        <div class="circle active_dot" id={year+"-dot"}></div>
      </div>
    {/each}
  </div>
  <div class="timeline-line"></div>
</div>
<div class="exp-display">
  <div class="exp-card">
    <div class="card-title">
      <img src="/icons/briefcase.svg" alt="Briefcase" class="card-icon"/>
      <span class="large-text card-title-text">{entries[choice].name}</span>
    </div>
    <span class="card-subtitle xs-text">
      Title: {entries[choice].title}
    </span>
    <span class="card-subtitle xs-text">
      Company: {entries[choice].company}
    </span>
    <span class="card-desc small-text">
      {entries[choice].desc}
    </span>
    <div class="card-date">
      {entries[choice].date}
    </div>
  </div>
  <div class="exp-nav-holder">
    <div class="counter small-text">
      {choice + 1}/{entries.length}
    </div>
    <div class="exp-nav">
      <div 
        class="nav-button"
        role="button"
        aria-pressed="false"
        tabindex="0"
        on:click={() => {
          choice = choice === 0 ? entries.length - 1 : choice - 1;
          renderTimeline();
        }}
        on:keydown={(e) => {
          if (e.key === "enter") {
            choice = choice === 0 ? entries.length - 1 : choice - 1;
            renderTimeline();
          }
        }}
      >
       <img src="/icons/arrowleft.svg" alt="Previous"/>
      </div>
      <div 
        class="nav-button flip-arr"
        role="button"
        aria-pressed="false"
        tabindex="0"
        on:click={() => {
          choice = choice === entries.length - 1 ? 0 : choice + 1;
          renderTimeline();
        }}
        on:keydown={(e) => {
          if (e.key === "enter") {
            choice = choice === entries.length - 1 ? 0 : choice + 1;
            renderTimeline();
          }
        }}
      >
       <img src="/icons/arrowleft.svg" alt="Next"/>
      </div>
    </div>
  </div>
</div>

<style>
  .exp-nav-holder {
    height: 10vh;
    width: 14vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
  }
  .exp-nav {
    height: 6vh;
    width: 12vh;
    display: flex;
  }
  .nav-button {
    transition: 0.2s;
  }
  .nav-button > img {
    height: 100%;
    aspect-ratio: 1/1;
    cursor: pointer;
    transition: 0.2s;
    filter: invert(1);
    --webkit-filter: invert(1);
  }
  .flip-arr {
    transform: rotate(180deg);
  }
  .nav-button:hover {
    transform: scale(1.1);
    background-color: color-mix(in srgb, var(--dark-grey) 15%, transparent 85%);
  }
  .nav-button > img:hover {
    transform: scale(1.1);
  }
  .flip-arr:hover {
    transform: rotate(180deg) scale(1.1);
  }

  .exp-display {
    min-height: 60vh;
    width: 100%;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
  }
  .card-date {
    font-size: clamp(0.5rem, 2vw, 0.75rem);
    color: color-mix(in srgb, var(--dark-grey) 35%, var(--font-color) 65%);
    margin-top: 4vh;
    margin-bottom: 2vh;
    text-align: left;
    margin-left: 0.75vw;
    width: 95%;
    min-height: 2vh;
    justify-self: flex-end;
  }

  .card-desc {
    color: var(--font-color);
    margin-top: 2vh;
    text-align: left;
    width: 90%;
    min-height: 10vh;
  }

  .card-subtitle {
    color: color-mix(in srgb, var(--dark-grey) 35%, var(--font-color) 65%);
    margin-top: 1vh;
    text-align: left;
    margin-left: 0.75vw;
    width: 95%;
    min-height: 2vh;
  }

  .card-title {
    width: 100%;
    margin-top: 2vh;
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: center;
  }
  .card-icon {
    height: 4vh;
    aspect-ratio: 1/1;
    margin-left: 0.75vw;
    margin-right: 0.75vw;
    filter: invert(.75);
    --webkit-filter: invert(.75);
  }
  .card-title-text {
    min-height: 5vh;
    text-align: left;
    color: var(--font-color);
  }
  .exp-card {
    width: 40%;
    border: 0.15vw solid var(--dark-grey);
    border-radius: 1vw;
    background-color: color-mix(in srgb, var(--dark-grey) 5%, transparent 95%);
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
  }


  .timeline-title {
    width: 100%;
    text-align: center;
    margin-bottom: 4vh;
  }
  .timeline-holder {
    --dot-color: color-mix(in srgb, var(--dark-grey) 80%, transparent 20%);
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    width: 100%;
  }
  .years {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    height: 6vh;
    width: 100%;
  }
  .year {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    height: 6vh;
    width: 6vh;
  }
  .year-text {
    height: 4.5vh;
    width: 100%;
    text-align: center;
    color: color-mix(in srgb, var(--dark-grey) 35%, var(--font-color) 65%);
  }
  .circle {
    background-color: var(--dot-color);
    border: 1px solid var(--dot-color);
    border-radius: 50%;
    height: 1.5vh;
    width: 1.5vh;
  }
  .active_dot {
    z-index: 1;
    transform: scale(1.5);
    background-color: var(--font-color);
    border: 1px solid var(--font-color);
  }
  .timeline-line {
    width: 100%;
    height: 1vh;
    border-top: 0.25vh dashed var(--dot-color);
    margin-top: -1vh;
  }
</style>