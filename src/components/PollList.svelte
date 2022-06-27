<script>
    import PollDetail from "./PollDetail.svelte"

    let polls = [];

    export {polls}
</script>
<div class="poll-list">
    {#if polls.length > 0}
        {#each polls as poll (poll.id)}
            <div>
                <PollDetail poll={poll} on:vote />
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