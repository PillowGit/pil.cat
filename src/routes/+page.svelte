<script lang="ts">
  //https://venmo.com/u/Aescart
  function copy_to_clipboard(text: string) {
    navigator.clipboard.writeText(text);
    alert("Copied to clipboard!");
  }
</script>

<title>Donate to Angelica</title>
<div class="cont">
  <h1 class="title">Send Angelica Graduation Money!!!</h1>

  <a href="https://venmo.com/u/Aescart" target="_blank" class="venmo">
    <div>
      <img src="/icons/venmo.svg" alt="Venmo" />
      <span>@Aescart</span>
    </div>
  </a>

  <!-- Should copy to clipboard on click -->
  <div
    class="zelle"
    role="button"
    aria-pressed="false"
    tabindex="0"
    on:click={() => copy_to_clipboard("3232362434")}
    on:keydown={(e) => {
      if (e.key === "Enter") {
        copy_to_clipboard("3232362434");
      }
    }}
  >
    <div>
      <img src="/icons/zelle.png" alt="Zelle" />
      <span>(323) 236 - 2434</span>
    </div>
  </div>

  <span class="footer">Website made by Esteban<br />(Click the buttons)</span>
</div>

<style>
  .cont {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-direction: column;
    position: absolute;
    top: 10%;
    left: 15%;
    height: 80%;
    width: 70%;
    min-width: 4rem;
  }
  .title {
    font-size: clamp(1.5rem, 5vw, 2.5rem);
    text-align: center;
  }
  .footer {
    font-size: clamp(0.75rem, 3vw, 1.25rem);
    color: color-mix(in srgb, var(--font-color) 75%, transparent 25%);
    text-align: center;
  }

  /* Venmo styling */
  .venmo {
    width: 100%;
    height: 10%;
    border-radius: 1rem;
    background-color: #3396cd;
    border: 0.15rem solid color-mix(in srgb, #3396cd 50%, black 50%);
    text-decoration: none;
    color: var(--font-color);
    font-size: clamp(1.25rem, 3vw, 1.75rem);
    font-style: bold;
  }
  .venmo > div {
    height: 100%;
    width: 100%;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: flex-start;
  }
  .venmo > div > img {
    height: 90%;
    aspect-ratio: 1/1;
    border-radius: 1rem;
  }
  .venmo > div > span {
    width: 100%;
    text-align: center;
  }

  /* Zelle styling */
  .zelle {
    width: 100%;
    height: 10%;
    border-radius: 1rem;
    background-color: #6c1cd3;
    border: 0.15rem solid color-mix(in srgb, #6c1cd3 50%, black 50%);
    text-decoration: none;
    color: var(--font-color);
    font-size: clamp(1.25rem, 3vw, 1.75rem);
    font-style: bold;
  }
  .zelle > div {
    height: 100%;
    width: 100%;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: flex-start;
  }
  .zelle > div > img {
    height: 90%;
    aspect-ratio: 1/1;
    border-radius: 1rem;
  }
  .zelle > div > span {
    width: 100%;
    text-align: center;
  }

  /* Debug styles */
  .cont {
    border: 1px solid red;
  }
  .title {
    border: 1px solid red;
  }
  .footer {
    border: 1px solid red;
  }
  div {
    border: 1px solid red;
  }
</style>
