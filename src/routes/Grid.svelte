<script lang='ts'>
  import { createEventDispatcher } from "svelte";
    import Square from "./Square.svelte";

    export let grid: string[];
    export let found: string[];
    
    const dispatch = createEventDispatcher();

    let a = -1;
    let b = -1;
    let reset_timeout: number
</script>

<div class="grid">
    
    {#each grid as emoji, i}
        <Square {emoji} on:click={()=>{
            clearTimeout(reset_timeout);
            if (a === - 1 && b === -1 ){
                a = i;
            } else if (b === -1) {
                b = i;
                if (grid[a] === grid[b]){
                    //correct
                    dispatch('found', {emoji});
                } else {
                    //it means the user didn't get it right
                    reset_timeout = setTimeout(()=>{
                        //we flip both 
                        a = b = -1 }, 1000);
                }
            } else {
                //if both of them are selected, it means that the user didn't get it right. so we need to flip over the second card
                a = i;
                b = -1;
            }
        }}
        selected={a === i || b === i}
        found={found.includes(emoji)}
        />
    {/each}

</div>

<style>
    .grid {
        display: grid;
        height: 100%;
        grid-gap: 0.5em;
        grid-template-columns: repeat(4, 1fr);
        grid-template-rows: repeat(4, 1fr);
        perspective: 100vw;
    }
</style>