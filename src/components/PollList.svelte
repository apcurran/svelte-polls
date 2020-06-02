<script>
    import PollStore from "../stores/PollStore.js";
    import PollDetails from "./PollDetails.svelte";

</script>

<div class="poll-list">
    <!-- $PollStore gets data from store -->
    {#each $PollStore as poll (poll.id)}
        <!-- Forward on:vote to parent component -->
        <PollDetails poll={poll} on:vote />
    {/each}
</div>

<style>
    .poll-list {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        gap: 1rem 1.25rem;
    }
</style>