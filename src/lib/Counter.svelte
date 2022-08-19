<script>
    export let like = 0;
    export let unlike = 0;
    export let inc = () => like++;
    export let dec = () => unlike--;

</script>
<div class="poll">
    <p>Cosa ne pensi?</p>
    <div class="poll__btn">
        <div class="poll__btn__box">
            <button on:click={inc}>&#128077;</button>
            <div>{like}</div>
        </div>
        <div class="poll__btn__box">
            <button on:click={dec}>&#128078;</button>
            <div>{unlike}</div>
        </div>
    </div>
    {#if like + unlike > 0}
        <p>Un numero > di {like} è sempre un successo</p>
    {:else if like + unlike < 0}
        <p>Le sconfitte aiutano a crescere!</p>
        {#if unlike < -4}
            <p>{unlike} ?? Si cresce troppo infretta così!!</p>
        {/if}
    {/if}
</div>
<style>
    .poll {
        font-size: 1.125rem;
        margin: 5rem auto;
    }
    .poll__btn {
        display: flex;
        justify-content: center;
        gap: var(--xxs);
    }
    .poll__btn__box div {
        margin-top: var(--xs);
    }
</style>
