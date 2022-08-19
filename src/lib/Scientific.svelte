<script>
export let op = (value) => {};
export let propValue;
const factorial = n => n != 1 ? (n * factorial(n-1)) : 1;
</script>
<div class="scientific">
    <button on:click={()=>op(Math.sqrt(propValue))}>&#8730;</button>
    <button on:click={()=>op(Math.cbrt(propValue))}><sup>3</sup>&#8730</button>
    <button on:click={()=>op(factorial(propValue))}>x!</button>
    <button on:click={()=>op(Math.tan(propValue))}>tan</button>
    <button on:click={()=>op(Math.sin(propValue))}>sin</button>
    <button on:click={()=>op(Math.cos(propValue))}>cos</button>
    <button on:click={()=>op(Math.log10(propValue))}>Log</button>
    <button on:click={()=>op(Math.pow(propValue, propValue))}>x<sup>(x)</sup></button>
    <button on:click={()=>op(Math.PI)}>&#960;</button>
</div>
<style>
    .scientific {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        grid-row: 1;
        gap: var(--xs);
        width: 12.5rem;
        background-color: var(--main-color-light);
    }
    button {
        background-color: var(--border-light);
        border-color: var(--bg-color-light);
        color: var(--bg-color-light);
        box-shadow: 2px 2px 2px #fff;
    }
</style>