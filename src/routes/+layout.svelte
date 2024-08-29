<html lang="en">
  <div class="page">
    <div class="padding"></div>
    <div class="container">
      <slot/>
    </div>
  </div>
</html>

<style>
  html {
    overflow: scroll;
    color: var(--font-color);
  }
  ::-webkit-scrollbar {
    width: 0px;
    background: transparent;
  }

  .page {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;

    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }
  .padding {
    width: 100%;
    height: clamp(0px, 10%, 100px);
  }
  .container {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;

    width: clamp(300px, 50%, 1400px);
  }
</style>