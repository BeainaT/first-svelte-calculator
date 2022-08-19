<script>
    export let input;
    export let result;
</script>
<div class="display">
    <div>{input}</div>
    {#if result !== 0 && result !== parseFloat(input)}
      <div class="big">{result}</div>
    {/if}
</div>

<style>
    .display {
        width: 15.625rem;
        overflow-wrap: break-word;
        min-height: 6.25rem;
        margin: var(--s) 0;
        border: inset;
        border-right: 1.5px solid grey;
        border-bottom: 1.5px solid grey;
        text-align: right;
        font-size: var(--ml);
        padding: var(--m);
        border-radius: 10px;
        background-color: var(--display-light);
        color: var(--bg-color-light);
        font-weight: 900;
    }
    .big {
        font-size: 3rem;
    }
</style>