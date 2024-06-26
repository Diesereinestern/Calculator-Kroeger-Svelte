<script lang="ts">
  import { onMount } from "svelte";
  import PageLoader from "./lib/PageLoader.svelte";

  let displayValue: string = "";
  let backendVal: string = "";
  let errorOccured: boolean = false;
  let loading: boolean = true;

  function appendValue(value: string) {
    const operators = ['+', '-', '*', '/'];

    // Check if the last character is an operator and the new value is also an operator
    if (operators.includes(backendVal.slice(-1)) && operators.includes(value)) {
      return; // Do not append the value
    }

    if (errorOccured) {
      clearDisplay();
      errorOccured = false;
    }
    backendVal += value;
    backendVal = insertMultiplicationSymbol(backendVal);
    transform();
  }

  function formatEquation(equation: string): string {
    const regex = /(\d+|\+|-|\*|\/|\^|\*\*|√\(\d*\))/g;

    const formatNumber = (num: string): string => {
      return num.replace(/\B(?=(\d{3})+(?!\d))/g, ".");
    };

    return equation.replace(regex, (match) => {
      return /\d/.test(match) ? formatNumber(match) : match;
    });
  }

  function insertMultiplicationSymbol(expression: any) {
    let result = "";
    for (let i = 0; i < expression.length; i++) {
      if (expression[i] === "(") {
        if (i > 0 && !isNaN(expression[i - 1])) {
          result += "*";
        }
      }
      result += expression[i];
    }
    return result;
  }

  function transform() {
    displayValue = backendVal
      .replace(/\//g, "÷")
      .replace(/\./g, ",")
      .replace(/\*/g, "×")
      .replace(/\^/g, "^")
      .replace(/Math.sqrt\(/g, "√(")
      .replace(/\)/g, ")");
    displayValue = formatEquation(displayValue);
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
      backendVal = String(
        eval(
          backendVal
            .replace("÷", "/")
            .replace("×", "*")
            .replace(/\^/g, "**")
            .replace(/√/g, "Math.sqrt")
        )
      );
      transform();
    } catch (error) {
      console.error(error);
      displayValue = "Error";
      errorOccured = true;
    }
  }

  function onKeyDown(e: any) {
    switch (e.key) {
      case "Backspace":
        deleteChar();
        break;
      case "=":
        calculate();
        break;
      case "Enter":
        calculate();
        break;
      case "c":
        clearDisplay();
        break;
      case "0":
        appendValue(e.key);
        break;
      case "1":
        appendValue(e.key);
        break;
      case "2":
        appendValue(e.key);
        break;
      case "3":
        appendValue(e.key);
        break;
      case "4":
        appendValue(e.key);
        break;
      case "5":
        appendValue(e.key);
        break;
      case "6":
        appendValue(e.key);
        break;
      case "7":
        appendValue(e.key);
        break;
      case "8":
        appendValue(e.key);
        break;
      case "9":
        appendValue(e.key);
        break;
      case "+":
        appendValue(e.key);
        break;
      case "-":
        appendValue(e.key);
        break;
      case "*":
        appendValue(e.key);
        break;
      case "/":
        appendValue(e.key);
        break;
      case "(":
        appendValue(e.key);
        break;
      case ")":
        appendValue(e.key);
        break;
      case ",":
        appendValue(".");
        break;
      case "^":
        appendValue(e.key);
        break;
      case "r":
        appendSquareRoot();
        break;
    }
  }

  function appendSquare() {
    if (errorOccured) {
      clearDisplay();
      errorOccured = false;
    }
    try {
      const lastNumberMatch = backendVal.match(/(\d+(\.\d+)?|\.\d+)(?=\D*$)/);
      if (lastNumberMatch) {
        const lastNumber = lastNumberMatch[0];
        const square = Math.pow(parseFloat(lastNumber), 2);
        backendVal = backendVal.replace(
          /(\d+(\.\d+)?|\.\d+)(?=\D*$)/,
          square.toString()
        );
        transform();
      }
    } catch (error) {
      console.error(error);
      displayValue = "Error";
      errorOccured = true;
    }
  }

  function appendSquareRoot() {
    if (errorOccured) {
      clearDisplay();
      errorOccured = false;
    }
    try {
      const lastNumberMatch = backendVal.match(/(\d+(\.\d+)?|\.\d+)(?=\D*$)/);
      if (lastNumberMatch) {
        const lastNumber = lastNumberMatch[0];
        const squareRoot = Math.sqrt(parseFloat(lastNumber));
        backendVal = backendVal.replace(
          /(\d+(\.\d+)?|\.\d+)(?=\D*$)/,
          squareRoot.toString()
        );
        transform();
      }
    } catch (error) {
      console.error(error);
      displayValue = "Error";
      errorOccured = true;
    }
  }

  function negateValue() {
    if (errorOccured) {
      clearDisplay();
      errorOccured = false;
    }
    try {
      const lastNumberMatch = backendVal.match(/(\-?\d+(\.\d+)?|\.\d+)(?=\D*$)/);
      if (lastNumberMatch) {
        const lastNumber = lastNumberMatch[0];
        const negatedNumber = parseFloat(lastNumber) * -1;
        backendVal = backendVal.replace(
          /(\-?\d+(\.\d+)?|\.\d+)(?=\D*$)/,
          negatedNumber.toString()
        );
        transform();
      }
    } catch (error) {
      console.error(error);
      displayValue = "Error";
      errorOccured = true;
    }
  }

  onMount(() => {
    setTimeout(() => {
      loading = false;
    }, 4000);
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
            style="background-color: #A2C9E6;"
            class="w-full px-4 py-2 mb-4 rounded-lg text-right text-black text-2xl outline-none"
          />
          <div class="grid grid-cols-4 gap-5">
            <button class="btn" on:click={() => appendValue("(")}>(</button>
            <button class="btn" on:click={() => appendValue(")")}>)</button>
            <button class="btn" on:click={clearDisplay}>C</button>
            <button class="btn" on:click={deleteChar}>DEL</button>
            <button class="btn" on:click={() => appendValue("^")}>^</button>
            <button class="btn" on:click={appendSquare}>x²</button>
            <button class="btn" on:click={appendSquareRoot}>√</button>
            <button class="btn" on:click={negateValue}>±</button>
            <button class="btn" on:click={() => appendValue("7")}>7</button>
            <button class="btn" on:click={() => appendValue("8")}>8</button>
            <button class="btn" on:click={() => appendValue("9")}>9</button>
            <button class="btn" on:click={() => appendValue("/")}>÷</button>
            <button class="btn" on:click={() => appendValue("4")}>4</button>
            <button class="btn" on:click={() => appendValue("5")}>5</button>
            <button class="btn" on:click={() => appendValue("6")}>6</button>
            <button class="btn" on:click={() => appendValue("*")}>×</button>
            <button class="btn" on:click={() => appendValue("1")}>1</button>
            <button class="btn" on:click={() => appendValue("2")}>2</button>
            <button class="btn" on:click={() => appendValue("3")}>3</button>
            <button class="btn" on:click={() => appendValue("-")}>-</button>
            <button class="btn" on:click={() => appendValue(".")}>,</button>
            <button class="btn" on:click={() => appendValue("0")}>0</button>

            <button class="btn" on:click={calculate}>=</button>
            <button class="btn" on:click={() => appendValue("+")}>+</button>
          </div>
        </div>
      </div>
    </div>
  {/if}
</main>

<svelte:window on:keydown|preventDefault={onKeyDown} />
