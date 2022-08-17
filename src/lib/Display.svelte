<script>
    export let input;
    export let result;
</script>
<div class="display">
    <!-- <slot></slot> -->
    <div>{input}</div>
    {#if result !== 0 && result !== parseFloat(input)}
      <div class="big">{result}</div>
    {/if}
</div>

<style>
    .display {
        width: 250px;
        overflow-wrap: break-word;
        min-height: 100px;
        margin: 5px 0;
        border: 2px solid #fff;
        text-align: right;
        font-size: 20px;
        padding: 20px;
        border-radius: 10px;
        background-color:  rgb(5, 5, 75);
        color: #fff;
    }
    .big {
        font-size: 32px;
    }
</style>