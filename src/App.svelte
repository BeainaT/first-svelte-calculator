<script>
  import Display from './lib/Display.svelte';

  let inputNumber = '';
  let total = 0;

  function getInput(value) {
    inputNumber += value.toString();
    total = eval(inputNumber);
  }  
  function clear() {
    total = 0;
    inputNumber = '';
  }
  const calc = () => total ? eval(inputNumber) : '';

</script>

<!-- <main> -->
  <h1>Calculator</h1>
    <Display>
      <div>{inputNumber}</div>
      {#if total !== 0 && total !== parseInt(inputNumber)}
        <div class="big">{total}</div>        
      {/if}
    </Display>
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
    <button on:click={calc}>=</button>
    <button on:click={clear}>C</button>
<!-- </main> -->

<style>
  button {
    border: 2px solid darkblue;
  }
  .big {
    font-size: 40px;
  }
</style>
