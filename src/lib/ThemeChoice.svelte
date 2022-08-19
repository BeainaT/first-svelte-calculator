<script>
    export let theme = true;
    export let toggle = () => theme = !theme;
    export let appTheme = () => {};
</script>
<span class="{theme ? 'hidden' : ''} toggle_theme">Preferisco calcolare al buio</span>
    <button on:click={toggle} on:click={appTheme}>
      {#if theme}
        &#9788;
      {:else}
        &#9790;
      {/if}
    </button>
<span class="{theme ? '' : 'hidden'} toggle_theme">Meglio accendere la luce</span>

<style>
    .toggle_theme {
    padding: var(--s);
    font-size: 1.125rem;
    }
    .hidden {
        opacity: 0;
        transition: 0.3s;
    }
</style>