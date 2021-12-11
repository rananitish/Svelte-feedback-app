<script>
import {fade,scale} from  'svelte/transition'
import FeedbackItems from "./FeedbackItems.svelte";

    export let feedback=[];
console.log(feedback)
</script>
{#each feedback as fb(fb.id) }
<div  in:scale out:fade>
    <FeedbackItems item={fb} on:delete-feedback/>
</div>

{/each}