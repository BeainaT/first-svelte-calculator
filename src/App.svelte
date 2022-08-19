<script>
  import Display from "./lib/Display.svelte";
  import Scientific from "./lib/Scientific.svelte";
  import Counter from "./lib/Counter.svelte";
  import ThemeChoice from "./lib/ThemeChoice.svelte";

  let inputNumber = "";
  let total = 0;
  let operators = ["+", "-", "*", "/"];
  let change = false;
  let rotate = false;
  let theme = false;

  function getInput(value) {
    if (isNaN(value)) {
      return (inputNumber += value);
    } else {
      inputNumber += value.toString();
      if (
        inputNumber.startsWith("0") &&
        isNaN(parseFloat(inputNumber.charAt(1))) == false
      ) {
        inputNumber = parseInt(inputNumber, 10).toString();
      }
    }
    return (total = eval(inputNumber));
  }
  function clear() {
    total = 0;
    inputNumber = "";
  }
  function undo() {
    if (inputNumber.length > 1) {
      inputNumber = inputNumber.slice(0, inputNumber.length - 1);
      let inputLast = inputNumber.charAt(inputNumber.length - 1);
      if (inputLast == operators.find((i) => i == inputLast)) {
        let removeInput = inputNumber.slice(0, inputNumber.length - 1);
        total = eval(removeInput);
      } else {
        total = eval(inputNumber);
      }
    } else {
      inputNumber = "";
      total = 0;
    }
  }
  function percentage() {
    total = total / 100;
    inputNumber = total.toString();
  }
  function exp() {
    return (inputNumber = total.toExponential());
  }
  function calc() {
    if (total) {
      total % 1 !== 0
        ? (total = eval(inputNumber).toFixed(2))
        : (total = eval(inputNumber));
      inputNumber = total.toString();
    }
    return (total = 0);
  }
  let toggle = () => (change = !change);
  let turns = () => (rotate = !rotate);

  let scientificOp = (value) =>
    value != Math.PI ? (total = value) : (inputNumber += value);

  let toggleTheme = () => (theme = !theme);
</script>

<div class="{!theme ? 'dark' : ''} app_container">
  <ThemeChoice trys={toggleTheme} />
  <main>
    <div class="{rotate ? 'rotate' : ''} calculator">
      <Display input={inputNumber} result={total} />
      <div class="keypad">
        <div class="keypad__body">
          <button on:click={() => getInput(1)}>1</button>
          <button on:click={() => getInput(2)}>2</button>
          <button on:click={() => getInput(3)}>3</button>
          <button on:click={() => getInput(4)}>4</button>
          <button on:click={() => getInput(5)}>5</button>
          <button on:click={() => getInput(6)}>6</button>
          <button on:click={() => getInput(7)}>7</button>
          <button on:click={() => getInput(8)}>8</button>
          <button on:click={() => getInput(9)}>9</button>
          <button on:click={() => getInput(".")}>,</button>
          <button on:click={() => getInput(0)}>0</button>
          <button on:click={clear}>C</button>
          <button on:click={percentage}>%</button>
          <button on:click={exp}>e</button>
          <button on:click={undo}>&#8656;</button>
        </div>
        <div class="keypad__op">
          <button on:click={() => getInput("+")}>+</button>
          <button on:click={() => getInput("-")}>-</button>
          <button on:click={() => getInput("/")}>/</button>
          <button on:click={() => getInput("*")}>*</button>
          <button on:click={calc}>=</button>
        </div>
      </div>
      {#if !rotate}
        <button class="switch" on:click={toggle}>
          <span>Scientific</span>
        </button>
        {#if change}
          <Scientific propValue={inputNumber} op={scientificOp} />
        {/if}
      {/if}
    </div>
    <div class="choice">
      <button on:click={turns}>
        {#if !rotate}
          <span>Back to 90s</span>
        {:else}
          <span>Back to 21<sup>th</sup>century</span>
        {/if}
      </button>
    </div>
  </main>
  <Counter />
</div>

<style>
  .app_container {
    margin: 0 auto;
    padding: 2rem;
    text-align: center;
    height: 100vh;
  }
  .calculator {
    background-color: var(--calc-color-light);
    padding: var(--lg) var(--lg);
    position: relative;
    color: var(--color-light);
    border-radius: var(--s);
    border: var(--calc-color-light) inset;
    box-shadow: var(--s) var(--s) var(--sm) var(--border-calc-light);
    border-bottom: 2px solid var(--border-out);
    border-right: 2px solid var(--border-out);
    transition: 1s;
  }

  .switch {
    background-color: var(--border-light);
    position: absolute;
    right: -1.5625rem;
    margin-top: var(--s);
    width: var(--xl);
    height: var(--xl);
    border-radius: 50%;
    padding: 0;
    opacity: 1;
  }
  .switch span {
    font-size: var(--s);
    line-height: var(--xl);
    color: var(--bg-color-light);
  }
  .keypad {
    display: grid;
    grid-template-areas: "n o";
    font-weight: bold;
    margin-bottom: var(--s);
    grid-gap: var(--s);
  }
  .keypad__body {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-area: n;
  }
  .keypad__op {
    display: grid;
    grid-template-columns: 1;
    font-weight: 900;
  }
  .keypad__body,
  .keypad__op {
    gap: var(--xxs);
  }
  .choice button {
    width: 12.5rem;
    padding: 0.6em 0;
  }
</style>
