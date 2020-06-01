<script>
    import PollDetails from "./PollDetails.svelte";
    export let polls = [];


</script>

<div class="poll-list">
    {#each polls as poll (poll.id)}
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