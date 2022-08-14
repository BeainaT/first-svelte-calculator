<script>
  import Display from './lib/Display.svelte';

  let inputNumber = '';
  let total = 0;
  let operators = ['+', '-', '*', '/'];

  function getInput(value) {
    if(isNaN(value)) {
      return inputNumber += value;
    } else {
      inputNumber += value.toString();
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

  function calc() {
    if(total) {
      total % 1 !== 0 ? total = eval(inputNumber).toFixed(4) : total = eval(inputNumber);
      inputNumber = total.toString();
    }
    return total = 0;
  }
</script>

<!-- <main> -->
  <h1>Calculator</h1>
    <Display>
      <div>{inputNumber}</div>
      {#if total !== 0 && total !== parseFloat(inputNumber)}
        <div class="big">{total}</div>        
      {/if}
    </Display>
    <div class="keypad">
      <button on:click={()=>getInput(1)}>1</button>
      <button on:click={()=>getInput(2)}>2</button>
      <button on:click={()=>getInput(3)}>3</button>
      <button on:click={()=>getInput(4)}>4</button>
      <button on:click={()=>getInput(5)}>5</button>
      <button on:click={()=>getInput(6)}>6</button>
      <button on:click={()=>getInput(7)}>7</button>
      <button on:click={()=>getInput(8)}>8</button>
      <button on:click={()=>getInput(9)}>9</button>
      <button on:click={()=>getInput(0)}>0</button>
      <button on:click={()=>getInput('+')}>+</button>
      <button on:click={()=>getInput('-')}>-</button>
      <button on:click={()=>getInput('/')}>/</button>
      <button on:click={()=>getInput('*')}>*</button>
      <button on:click={()=>getInput('.')}>,</button>
      <button on:click={undo}>ret</button>
      <button on:click={calc}>=</button>
      <button on:click={clear}>C</button>
    </div>
<!-- </main> -->

<style>
  button {
    border: 2px solid darkblue;
  }
  .big {
    font-size: 40px;
  }
  .keypad {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
  }
</style>
