<script>
  //https://venmo.com/u/Aescart
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

  <span class="footer">Made by Esteban</span>
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

  /* Debug styles 
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
*/
</style>
