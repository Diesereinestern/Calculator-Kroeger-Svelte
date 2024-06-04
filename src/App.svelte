<script lang="ts">
  import { onMount } from "svelte";
  import PageLoader from "./lib/PageLoader.svelte";

  let displayValue: string = "";
  let backendVal: string = "";
  let errorOccured: boolean = false;
  let loading: boolean = true;

  function appendValue(value: string) {
    if (errorOccured) {
      clearDisplay();
      errorOccured = false;
    }
    backendVal += value;
    transform();
  }

  function transform() {
    displayValue = backendVal.replace(/\//g, "÷").replace(/\./g, ",").replace(/\*/g, "×");
  }

  function clearDisplay() {
    displayValue = "";
    backendVal = "";
  }

  function deleteChar() {
    backendVal = backendVal.slice(0, -1);
    transform();
  }

  function calculate() {
    try {
      backendVal = String(eval(backendVal.replace("÷", "/").replace("×", "*")));
      transform();
    } catch (error) {
      console.error(error);
      displayValue = "Error";
      errorOccured = true;
    }
  }

  onMount(() => {
    setTimeout(() => {
      loading = false;
    }, 8200); // Loader duration set to 3.5 seconds
  });
</script>

<main>
  {#if loading}
    <PageLoader />
  {:else}
    <div class="content show">
      <div
        class="calculator bg-gray-800 rounded-lg p-8 shadow-lg text-white text-center flex"
      >
        <div>
          <input
            type="text"
            bind:value={displayValue}
            disabled
            class="w-full px-4 py-2 mb-4 bg-gray-700 rounded-lg text-right text-white text-2xl outline-none"
          />
          <div class="grid grid-cols-4 gap-5">
            <button class="btn" on:click={() => appendValue("(")}>(</button>
            <button class="btn" on:click={() => appendValue(")")}>)</button>
            <button class="btn" on:click={clearDisplay}>C</button>
            <button class="btn" on:click={deleteChar}>DEL</button>
            <button class="btn" on:click={() => appendValue("7")}>7</button>
            <button class="btn" on:click={() => appendValue("8")}>8</button>
            <button class="btn" on:click={() => appendValue("9")}>9</button>
            <button class="btn" on:click={() => appendValue("/")}>÷</button>
            <button class="btn" on:click={() => appendValue("4")}>4</button>
            <button class="btn" on:click={() => appendValue("5")}>5</button>
            <button class="btn" on:click={() => appendValue("6")}>6</button>
            <button class="btn" on:click={() => appendValue("*")}>x</button>
            <button class="btn" on:click={() => appendValue("1")}>1</button>
            <button class="btn" on:click={() => appendValue("2")}>2</button>
            <button class="btn" on:click={() => appendValue("3")}>3</button>
            <button class="btn" on:click={() => appendValue("-")}>-</button>
            <button class="btn" on:click={() => appendValue("0")}>0</button>
            <button class="btn" on:click={() => appendValue(".")}>.</button>
            <button class="btn" on:click={calculate}>=</button>
            <button class="btn" on:click={() => appendValue("+")}>+</button>
          </div>
        </div>
      </div>
    </div>
  {/if}
</main>
{#if loading}
<div class="stars">
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
  <div class="star"></div>
</div>
{/if}
<style>


.stars {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 120%;
  transform: rotate(-45deg);
}

.star {
  --star-color: var(--primary-color);
  --star-tail-length: 6em;
  --star-tail-height: 2px;
  --star-width: calc(var(--star-tail-length) / 6);
  --fall-duration: 10s; /* Change duration to 10 seconds */
  --tail-fade-duration: var(--fall-duration);
  position: absolute;
  top: var(--top-offset);
  left: 0;
  width: var(--star-tail-length);
  height: var(--star-tail-height);
  color: var(--star-color);
  background: linear-gradient(45deg, currentColor, transparent);
  border-radius: 50%;
  filter: drop-shadow(0 0 6px currentColor);
  transform: translate3d(104em, 0, 0);
  animation: fall var(--fall-duration) 0s linear , tail-fade var(--tail-fade-duration) 0s ease-out infinite;
}

@media screen and (max-width: 750px) {
  .star {
    animation: fall var(--fall-duration) 0s linear ;
  }
}

.star:nth-child(1) {
  --star-tail-length: 5.47em;
  --top-offset: 12.6vh;
  --fall-duration: 11.84s;
  --fall-delay: 4.572s;
}
.star:nth-child(2) {
  --star-tail-length: 5.22em;
  --top-offset: 68.25vh;
  --fall-duration: 7.516s;
  --fall-delay: 1.539s;
}
.star:nth-child(3) {
  --star-tail-length: 6.11em;
  --top-offset: 14.71vh;
  --fall-duration: 7.545s;
  --fall-delay: 7.857s;
}
.star:nth-child(4) {
  --star-tail-length: 6.94em;
  --top-offset: 96.82vh;
  --fall-duration: 6.187s;
  --fall-delay: 2.307s;
}
.star:nth-child(5) {
  --star-tail-length: 5.91em;
  --top-offset: 57.83vh;
  --fall-duration: 10.564s;
  --fall-delay: 3.514s;
}
.star:nth-child(6) {
  --star-tail-length: 6.81em;
  --top-offset: 33.66vh;
  --fall-duration: 11.265s;
  --fall-delay: 5.649s;
}
.star:nth-child(7) {
  --star-tail-length: 7.41em;
  --top-offset: 76.49vh;
  --fall-duration: 7.384s;
  --fall-delay: 2.779s;
}
.star:nth-child(8) {
  --star-tail-length: 6.66em;
  --top-offset: 5.64vh;
  --fall-duration: 9.465s;
  --fall-delay: 4.34s;
}
.star:nth-child(9) {
  --star-tail-length: 6.07em;
  --top-offset: 39.18vh;
  --fall-duration: 6.233s;
  --fall-delay: 5.508s;
}
.star:nth-child(10) {
  --star-tail-length: 5.37em;
  --top-offset: 85.6vh;
  --fall-duration: 10.271s;
  --fall-delay: 0.688s;
}
.star:nth-child(11) {
  --star-tail-length: 5.14em;
  --top-offset: 12.6vh;
  --fall-duration: 9.094s;
  --fall-delay: 7.909s;
}
.star:nth-child(12) {
  --star-tail-length: 7.39em;
  --top-offset: 6.21vh;
  --fall-duration: 8.31s;
  --fall-delay: 8.691s;
}
.star:nth-child(13) {
  --star-tail-length: 6.69em;
  --top-offset: 75.16vh;
  --fall-duration: 11.499s;
  --fall-delay: 4.646s;
}
.star:nth-child(14) {
  --star-tail-length: 7.03em;
  --top-offset: 64.42vh;
  --fall-duration: 6.918s;
  --fall-delay: 8.928s;
}
.star:nth-child(15) {
  --star-tail-length: 5.87em;
  --top-offset: 80.34vh;
  --fall-duration: 6.546s;
  --fall-delay: 9.156s;
}
.star:nth-child(16) {
  --star-tail-length: 5.7em;
  --top-offset: 29.34vh;
  --fall-duration: 11.55s;
  --fall-delay: 4.638s;
}
.star:nth-child(17) {
  --star-tail-length: 7.42em;
  --top-offset: 15.7vh;
  --fall-duration: 10.84s;
  --fall-delay: 2.039s;
}
.star:nth-child(18) {
  --star-tail-length: 6.4em;
  --top-offset: 60.7vh;
  --fall-duration: 7.988s;
  --fall-delay: 2.259s;
}
.star:nth-child(19) {
  --star-tail-length: 6.7em;
  --top-offset: 65.46vh;
  --fall-duration: 10.571s;
  --fall-delay: 2.335s;
}
.star:nth-child(20) {
  --star-tail-length: 5.25em;
  --top-offset: 41.39vh;
  --fall-duration: 10.333s;
  --fall-delay: 2.317s;
}
.star:nth-child(21) {
  --star-tail-length: 7.13em;
  --top-offset: 49.49vh;
  --fall-duration: 10.159s;
  --fall-delay: 0.348s;
}
.star:nth-child(22) {
  --star-tail-length: 6.77em;
  --top-offset: 74.62vh;
  --fall-duration: 8.161s;
  --fall-delay: 7.707s;
}
.star:nth-child(23) {
  --star-tail-length: 6.63em;
  --top-offset: 42.57vh;
  --fall-duration: 6.466s;
  --fall-delay: 4.864s;
}
.star:nth-child(24) {
  --star-tail-length: 6.11em;
  --top-offset: 42.46vh;
  --fall-duration: 6.377s;
  --fall-delay: 7.23s;
}
.star:nth-child(25) {
  --star-tail-length: 7.46em;
  --top-offset: 74.51vh;
  --fall-duration: 6.874s;
  --fall-delay: 3.094s;
}
.star:nth-child(26) {
  --star-tail-length: 5.9em;
  --top-offset: 60.54vh;
  --fall-duration: 11.692s;
  --fall-delay: 9.037s;
}
.star:nth-child(27) {
  --star-tail-length: 5.08em;
  --top-offset: 28.42vh;
  --fall-duration: 8.064s;
  --fall-delay: 0.708s;
}
.star:nth-child(28) {
  --star-tail-length: 6.91em;
  --top-offset: 51.79vh;
  --fall-duration: 8.321s;
  --fall-delay: 0.15s;
}
.star:nth-child(29) {
  --star-tail-length: 6.22em;
  --top-offset: 5.11vh;
  --fall-duration: 10.11s;
  --fall-delay: 0.169s;
}
.star:nth-child(30) {
  --star-tail-length: 5.73em;
  --top-offset: 84.17vh;
  --fall-duration: 11.383s;
  --fall-delay: 1.969s;
}
.star:nth-child(31) {
  --star-tail-length: 6.97em;
  --top-offset: 86.94vh;
  --fall-duration: 6.63s;
  --fall-delay: 4.187s;
}
.star:nth-child(32) {
  --star-tail-length: 5.85em;
  --top-offset: 51.07vh;
  --fall-duration: 10.46s;
  --fall-delay: 6.788s;
}
.star:nth-child(33) {
  --star-tail-length: 6.05em;
  --top-offset: 87.06vh;
  --fall-duration: 7.939s;
  --fall-delay: 1.796s;
}
.star:nth-child(34) {
  --star-tail-length: 6.16em;
  --top-offset: 29.55vh;
  --fall-duration: 7.879s;
  --fall-delay: 6.265s;
}
.star:nth-child(35) {
  --star-tail-length: 5.38em;
  --top-offset: 16.33vh;
  --fall-duration: 10.168s;
  --fall-delay: 1.352s;
}
.star:nth-child(36) {
  --star-tail-length: 5.58em;
  --top-offset: 83vh;
  --fall-duration: 6.89s;
  --fall-delay: 4.424s;
}
.star:nth-child(37) {
  --star-tail-length: 5.17em;
  --top-offset: 74.15vh;
  --fall-duration: 11.852s;
  --fall-delay: 0.252s;
}
.star:nth-child(38) {
  --star-tail-length: 5.59em;
  --top-offset: 24.86vh;
  --fall-duration: 6.428s;
  --fall-delay: 4.704s;
}
.star:nth-child(39) {
  --star-tail-length: 5.23em;
  --top-offset: 63.95vh;
  --fall-duration: 9.797s;
  --fall-delay: 6.062s;
}
.star:nth-child(40) {
  --star-tail-length: 7.25em;
  --top-offset: 56.43vh;
  --fall-duration: 11.33s;
  --fall-delay: 6.274s;
}
.star:nth-child(41) {
  --star-tail-length: 5.86em;
  --top-offset: 96.98vh;
  --fall-duration: 10.776s;
  --fall-delay: 9.637s;
}
.star:nth-child(42) {
  --star-tail-length: 6.84em;
  --top-offset: 2.88vh;
  --fall-duration: 9.526s;
  --fall-delay: 0.585s;
}
.star:nth-child(43) {
  --star-tail-length: 6.63em;
  --top-offset: 83.61vh;
  --fall-duration: 9.302s;
  --fall-delay: 5.624s;
}
.star:nth-child(44) {
  --star-tail-length: 5.26em;
  --top-offset: 46.43vh;
  --fall-duration: 6.601s;
  --fall-delay: 1.44s;
}
.star:nth-child(45) {
  --star-tail-length: 6.56em;
  --top-offset: 57.55vh;
  --fall-duration: 8.685s;
  --fall-delay: 3.539s;
}
.star:nth-child(46) {
  --star-tail-length: 6.31em;
  --top-offset: 75.62vh;
  --fall-duration: 8.654s;
  --fall-delay: 8.682s;
}
.star:nth-child(47) {
  --star-tail-length: 6.96em;
  --top-offset: 17.94vh;
  --fall-duration: 9.59s;
  --fall-delay: 2.937s;
}
.star:nth-child(48) {
  --star-tail-length: 6.7em;
  --top-offset: 68vh;
  --fall-duration: 6.942s;
  --fall-delay: 1.463s;
}
.star:nth-child(49) {
  --star-tail-length: 5.5em;
  --top-offset: 24.04vh;
  --fall-duration: 9.91s;
  --fall-delay: 6.723s;
}
.star:nth-child(50) {
  --star-tail-length: 6.09em;
  --top-offset: 14.13vh;
  --fall-duration: 10.344s;
  --fall-delay: 5.569s;
}
.star:nth-child(51) {
  --star-tail-length: 6.8em;
  --top-offset: 52.11vh;
  --fall-duration: 9.785s;
  --fall-delay: 0.879s;
}
.star:nth-child(52) {
  --star-tail-length: 6.2em;
  --top-offset: 38.17vh;
  --fall-duration: 11.215s;
  --fall-delay: 4.928s;
}
.star:nth-child(53) {
  --star-tail-length: 5.9em;
  --top-offset: 66.54vh;
  --fall-duration: 8.784s;
  --fall-delay: 7.55s;
}
.star:nth-child(54) {
  --star-tail-length: 7.4em;
  --top-offset: 26.93vh;
  --fall-duration: 8.154s;
  --fall-delay: 5.986s;
}
.star:nth-child(55) {
  --star-tail-length: 6.3em;
  --top-offset: 49.35vh;
  --fall-duration: 10.471s;
  --fall-delay: 2.759s;
}
.star:nth-child(56) {
  --star-tail-length: 6.7em;
  --top-offset: 88.69vh;
  --fall-duration: 9.42s;
  --fall-delay: 6.236s;
}
.star:nth-child(57) {
  --star-tail-length: 5.5em;
  --top-offset: 19.8vh;
  --fall-duration: 10.56s;
  --fall-delay: 9.445s;
}
.star:nth-child(58) {
  --star-tail-length: 5.9em;
  --top-offset: 44.27vh;
  --fall-duration: 7.548s;
  --fall-delay: 5.844s;
}
.star:nth-child(59) {
  --star-tail-length: 6.3em;
  --top-offset: 77.47vh;
  --fall-duration: 11.784s;
  --fall-delay: 8.111s;
}
.star:nth-child(60) {
  --star-tail-length: 6.7em;
  --top-offset: 5.96vh;
  --fall-duration: 8.829s;
  --fall-delay: 1.837s;
}
.star:nth-child(61) {
  --star-tail-length: 5.3em;
  --top-offset: 61.98vh;
  --fall-duration: 10.953s;
  --fall-delay: 5.054s;
}
.star:nth-child(62) {
  --star-tail-length: 6.7em;
  --top-offset: 38.42vh;
  --fall-duration: 9.072s;
  --fall-delay: 4.761s;
}
.star:nth-child(63) {
  --star-tail-length: 6.9em;
  --top-offset: 71.07vh;
  --fall-duration: 7.543s;
  --fall-delay: 1.981s;
}
.star:nth-child(64) {
  --star-tail-length: 7.1em;
  --top-offset: 24.86vh;
  --fall-duration: 11.832s;
  --fall-delay: 8.663s;
}
.star:nth-child(65) {
  --star-tail-length: 6.3em;
  --top-offset: 56.66vh;
  --fall-duration: 6.37s;
  --fall-delay: 4.677s;
}
.star:nth-child(66) {
  --star-tail-length: 5.8em;
  --top-offset: 85.09vh;
  --fall-duration: 10.085s;
  --fall-delay: 2.289s;
}
.star:nth-child(67) {
  --star-tail-length: 5.4em;
  --top-offset: 47.69vh;
  --fall-duration: 8.469s;
  --fall-delay: 2.939s;
}
.star:nth-child(68) {
  --star-tail-length: 5.6em;
  --top-offset: 69.92vh;
  --fall-duration: 6.928s;
  --fall-delay: 1.12s;
}
.star:nth-child(69) {
  --star-tail-length: 6.4em;
  --top-offset: 9.64vh;
  --fall-duration: 7.467s;
  --fall-delay: 0.349s;
}
.star:nth-child(70) {
  --star-tail-length: 5.9em;
  --top-offset: 37.77vh;
  --fall-duration: 11.052s;
  --fall-delay: 8.476s;
}
.star:nth-child(71) {
  --star-tail-length: 5.2em;
  --top-offset: 84.77vh;
  --fall-duration: 10.722s;
  --fall-delay: 4.848s;
}
.star:nth-child(72) {
  --star-tail-length: 5.3em;
  --top-offset: 15.67vh;
  --fall-duration: 7.975s;
  --fall-delay: 1.445s;
}
.star:nth-child(73) {
  --star-tail-length: 7.2em;
  --top-offset: 67.25vh;
  --fall-duration: 9.025s;
  --fall-delay: 3.946s;
}
.star:nth-child(74) {
  --star-tail-length: 5.9em;
  --top-offset: 48.34vh;
  --fall-duration: 7.147s;
  --fall-delay: 6.413s;
}
.star:nth-child(75) {
  --star-tail-length: 6.1em;
  --top-offset: 83.02vh;
  --fall-duration: 11.086s;
  --fall-delay: 3.344s;
}
.star:nth-child(76) {
  --star-tail-length: 6.6em;
  --top-offset: 27.76vh;
  --fall-duration: 6.233s;
  --fall-delay: 4.869s;
}
.star:nth-child(77) {
  --star-tail-length: 7.3em;
  --top-offset: 58.6vh;
  --fall-duration: 6.649s;
  --fall-delay: 1.156s;
}
.star:nth-child(78) {
  --star-tail-length: 5.5em;
  --top-offset: 95.63vh;
  --fall-duration: 8.034s;
  --fall-delay: 4.219s;
}
.star::before, .star::after {
  position: absolute;
  content: "";
  top: 0;
  left: calc(var(--star-width) / -2);
  width: var(--star-width);
  height: 100%;
  background: linear-gradient(45deg, transparent, currentColor, transparent);
  border-radius: inherit;
  animation: blink 2s linear infinite;
}
.star::before {
  transform: rotate(45deg);
}
.star::after {
  transform: rotate(-45deg);
}

@keyframes fall {
  to {
    transform: translate3d(-30em, 0, 0);
  }
}
@keyframes tail-fade {
  0%, 50% {
    width: var(--star-tail-length);
    opacity: 1;
  }
  70%, 80% {
    width: 0;
    opacity: 0.4;
  }
  100% {
    width: 0;
    opacity: 0;
  }
}
@keyframes blink {
  50% {
    opacity: 0.6;
  }
}
</style>