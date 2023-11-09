<script lang='ts'>
  import { get_twemoji_url } from "./utils";

    export let emoji: string;
    export let selected: boolean;
    export let found: boolean;
</script>

<div class="square" class:flipped = {selected}>
    <button on:click></button>

    <div class="background"></div>

    {#if !found}
        <img alt={emoji} src={get_twemoji_url(emoji)}/>
    {/if}
</div>

<style>
    .square {
        display: flex;
        justify-content: center;
        align-items: center;
        background: yellow;
    }

    button {
        position: absolute;
        height: 100%;
        width: 100%;
    }

    .background {
        background: #eee;
    }

    img {
        height: 6em;
        width: 6em;
        pointer-events: none;
    }

    .flipped {
        background: #eee;
    }
</style>