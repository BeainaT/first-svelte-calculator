<script>
  import Display from './lib/Display.svelte';
  import Scientific from './lib/Scientific.svelte';

  let inputNumber = '';
  let total = 0;
  let operators = ['+', '-', '*', '/'];
  let change = false;
  let rotate = false;
  let theme = false;

  function getInput(value) {
    if(isNaN(value)) {
      return inputNumber += value;
    } else {
      inputNumber += value.toString();
      if(inputNumber.startsWith('0') && isNaN(parseFloat(inputNumber.charAt(1))) == false) {
        inputNumber = parseInt(inputNumber, 10).toString();
      }
    }
    return total = eval(inputNumber);
  }  
  function clear() {
    total = 0;
    inputNumber = '';
  }
  function undo() {
    if(inputNumber.length > 1) {
      inputNumber = inputNumber.slice(0, inputNumber.length -1);
      let inputLast = inputNumber.charAt(inputNumber.length -1);
      if(inputLast == operators.find((i)=> i == inputLast)) {
        let removeInput = inputNumber.slice(0, inputNumber.length -1);
        total = eval(removeInput);
      } else {
        total = eval(inputNumber)
      }
    } else {
      inputNumber = '';
      total = 0;
    }
  }
  function percentage() {
    total = total / 100;
    inputNumber = total.toString();
  }
  function exp() {
    return inputNumber = total.toExponential();
  }
  function calc() {
    if(total) {
      (total % 1 !== 0) ? total = eval(inputNumber).toFixed(2) : total = eval(inputNumber);
      inputNumber = total.toString();
    }
    return total = 0;
  }
  let toggle = () => change = !change;
  let turns = () => rotate = !rotate;

  let scientificOp = (value) => value != Math.PI ? total = value : inputNumber += value;

  let toggleTheme = () => theme = !theme;
</script>

  <div class="{theme ? 'dark' : ''} app_container">  
    <button on:click={toggleTheme}>
      {#if theme}
        &#9788;
      {:else}
        &#9790;
      {/if}
    </button>
    <main>
      <div class="{rotate ? 'rotate' : ''} calculator">
        <Display input={inputNumber} result={total}/>
        <div class="keypad">
          <div class="keypad__body">
            <button on:click={()=>getInput(1)}>1</button>
            <button on:click={()=>getInput(2)}>2</button>
            <button on:click={()=>getInput(3)}>3</button>
            <button on:click={()=>getInput(4)}>4</button>
            <button on:click={()=>getInput(5)}>5</button>
            <button on:click={()=>getInput(6)}>6</button>
            <button on:click={()=>getInput(7)}>7</button>
            <button on:click={()=>getInput(8)}>8</button>
            <button on:click={()=>getInput(9)}>9</button>
            <button on:click={()=>getInput('.')}>,</button>
            <button on:click={()=>getInput(0)}>0</button>
            <button on:click={clear}>C</button>
            <button on:click={percentage}>%</button>
            <button on:click={exp}>e</button>
            <button on:click={undo}>&#8656;</button>
          </div>
          <div class="keypad__op">
            <button on:click={()=>getInput('+')}>+</button>
            <button on:click={()=>getInput('-')}>-</button>
            <button on:click={()=>getInput('/')}>/</button>
            <button on:click={()=>getInput('*')}>*</button>  
            <button on:click={calc}>=</button>
          </div>
        </div>
        {#if !rotate}
          <button class="switch" on:click={toggle}>
            <span>Scientific</span>
          </button>
          {#if change}
            <Scientific propValue={inputNumber} op={scientificOp}/>        
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
  </div>
  


<style>
  .app_container {
    margin: 0 auto;
    padding: 2rem;
    text-align: center;
    height: calc(100vh - 65.5px);
  }
  .calculator {
    background-color: var(--calc-color-light);
    padding: 30px 30px;
    position: relative;
    color: var(--color-light);
    border-radius: 10px;
    border: var(--calc-color-light) inset;
    box-shadow: 10px 10px 15px var(--border-calc-light);
    border-bottom: 2px solid var(--border-out);
    border-right: 2px solid var(--border-out);
    transition: 1s;
  }

  .switch {
    background-color: var(--border-light);
    position: absolute;
    right: -25px;
    margin-top: 10px;
    width: 50px;
    height: 50px;
    border-radius: 50%;
    padding: 0;
    opacity: 1;
  }
  .switch span {
    font-size: 10px;
    line-height: 50px;
    color: var(--bg-color-light);
  }
  .keypad {
    display: grid;
    grid-template-areas: "n o";
    font-weight: bold;
    margin-bottom: 10px;
    grid-gap: 10px;
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
    gap: 5px;
  }
  .choice {
    position: absolute;
    top: 50%;
    right: 5%;
  }
  .choice button {
    width: 200px;
    padding: 0.6em 0;
  }
</style>
