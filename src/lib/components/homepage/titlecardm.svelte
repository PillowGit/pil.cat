<script lang="ts">
  const githubpfp: string = "https://github.com/PillowGit.png";

  interface Social {
    name: string;
    user: string;
    link: string;
    icon: string;
  }
  const socials: Social[] = [
    {
      name: "Github",
      user: "PillowGit",
      link: "https://github.com/PillowGit",
      icon: "/icons/github.svg"
    },
    // {
    //   name: "LinkedIn",
    //   user: "na",
    //   link: "na",
    //   icon: "/icons/linkedin.svg"
    // },
    {
      name: "Instagram",
      user: "@PillowiGuess",
      link: "https://www.instagram.com/pillowiguess/",
      icon: "/icons/instagram.svg"
    },
    {
      name: "Spotify",
      user: "Pillow",
      link: "https://open.spotify.com/user/w4kn7ou1m1tnziicyppza0k3n",
      icon: "/icons/spotify.svg"
    },
    {
      name: "Gmail",
      user: "e.f.escartin@gmail.com",
      link: "mailto:e.f.escartin@gmail.com",
      icon: "/icons/gmail.svg"
    },
    {
      name: "Discord",
      user: "@pillo.",
      link: "https://discordapp.com/users/407963398207176715",
      icon: "/icons/discord.svg"
    }
  ]
</script>

<img src={githubpfp} alt="Github Profile Pic" class="github-pfp"/>
<div class="title-text title">
  Hi, I'm Esteban
</div>
<div class="xs-text subtitle">(aka Pillow)</div>
<div class="container">
  <div class="desc">
    <span class="xs-text desc-title">
      Software Developer, Google SWE Intern & CSUF 4th Year
    </span>
    <div class="desc-sep"></div>
    <span class="xs-text desc-desc">
      My name's Esteban, but I go by Pillow online. I'm a 4th year CS student at
      CSUF. I interned at Google Canada during summer 2024, with most my 
      experience being in AR and Calibration. I like reading manga, gaming, and
      grinding leetcode.
    </span>
  </div>
  <div class="socials">
    {#each socials as social}
      <div
        class="social"
        role="button"
        aria-pressed="false"
        tabindex="0"
        on:click={() => window.open(social.link)}
        on:keydown={(e) => {
          if (e.key === "enter") {
            window.open(social.link);
          }
        }}
      >
        <div class="soc-align-left">
          <img
            src={social.icon}
            alt={social.name}
            class={social.name === "Github" ? "icon github-invert" : "icon"}
          />
        </div>
        <div class="social-sep"></div>
        <div class="soc-align-right">
          <div class="xs-text soc-text">{social.user}</div>
        </div>
      </div>
    {/each}
  </div>
</div>

<style>
  .github-pfp {
    border: 3px solid var(--dark-grey);
    aspect-ratio: 1/1;
    border-radius: 50%;
    margin-bottom: 2vh;
    margin-top: 8vh;
    width: 30%;
  }

  .title {
    text-align: left;
    height: 5vh;
    width: 100%;
  }
  .subtitle {
    text-align: left;
    margin-bottom: 2vh;
    height: 3vh;
    width: 100%;
    color: color-mix(in srgb, var(--dark-grey) 35%, var(--font-color) 65%);
  }

  .container {
    display: flex;
    flex-direction: column;
  }

  .desc {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100%;
    width: 100%;
    margin-bottom: 3vh;
  }
  .desc-title {
    text-align: left;
    width: 100%;
    font-weight: bold;
  }
  .desc-sep {
    background-color: var(--dark-grey);
    margin-bottom: 3%;
    margin-top: 3%;
    height: 1px;
    width: 90%;
  }
  .desc-desc {
    color: color-mix(in srgb, var(--dark-grey) 35%, var(--font-color) 65%);
    text-align: left;
    width: 100%;
  }
  
  .socials {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    width: 100%;
  }
  .social {
    border: 0px solid var(--dark-grey);
    display: grid;
    grid-template-columns: 44.5% 1% 44.5%;
    width: 100%;
    height: 5vh;
    transition: 0.3s;
    margin-bottom: 1vh;
  }
  .social:hover {
    transform: scale(1.07);
    cursor: pointer;
    border: 1px solid var(--dark-grey);
    background-color: color-mix(in srgb, var(--dark-grey) 15%, transparent 85%);
  }
  .soc-align-left {
    height: 100%;
    width: 90%;
    display: flex;
    justify-content: flex-end;
    align-items: center;
  }
  .soc-align-right {
    height: 100%;
    width: 90%;
    margin-left: 10%;
    display: flex;
    justify-content: flex-start;
    align-items: center;
  }
  .icon {
    aspect-ratio: 1/1;
    height: 2rem;
  }
  .github-invert {
    filter: invert(1);
  }
  .social-sep {
    background-color: var(--dark-grey);
    height: 100%;
    width: 25%;
  }
  .soc-text {
    color: color-mix(in srgb, var(--dark-grey) 35%, var(--font-color) 65%);
  }
</style>
