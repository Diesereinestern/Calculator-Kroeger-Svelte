<div class="page-loader">
  <div class="star">
    <svg
      xmlns="http://www.w3.org/2000/svg"
      height="44px"
      viewBox="0 -960 960 960"
      width="44px"
      fill="#e8eaed"
      ><path
        d="m354-287 126-76 126 77-33-144 111-96-146-13-58-136-58 135-146 13 111 97-33 143ZM233-120l65-281L80-590l288-25 112-265 112 265 288 25-218 189 65 281-247-149-247 149Zm247-350Z"
      /></svg
    >
  </div>
  <div class="txt">Lennart Sojka<br />Development with ❤️</div>
</div>

<style>
  @import url("https://fonts.googleapis.com/css?family=Raleway&display=swap");

  html,
  body {
    position: relative;
    background-size: cover;
    height: 100vh;
    font-family: "Raleway", sans-serif;
    overflow-y: hidden;
  }

  /* PRELOADER CSS */
  .page-loader {
    border-radius: 10%;
    z-index: 1000;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: white;
  }

  .txt {
    text-transform: uppercase;
    letter-spacing: 0.3rem;
    font-weight: bold;
    line-height: 1.5;
  }

  /* SPINNER ANIMATION */
  .star {
    animation: spin 1.5s infinite ease-in-out;
  }

  @keyframes spin {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
</style>
