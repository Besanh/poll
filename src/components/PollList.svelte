<script>
    import { fade, slide, scale } from "svelte/transition";
    import { flip } from "svelte/animate";
    import PollDetail from "./PollDetail.svelte";
    import PollStore from "../stores/PollStore";

    let polls = [];
</script>

<div class="poll-list">
    {#if $PollStore.length > 0}
        {#each $PollStore as poll (poll.id)}
            <div in:fade out:scale|local animate:flip={{ duration: 500 }}>
                <PollDetail {poll} on:vote />
            </div>
        {/each}
    {:else}
        <p>No poll list</p>
    {/if}
</div>

<style>
    .poll-list {
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-gap: 20px;
    }
</style>
