<script>
    import { fade } from "svelte/transition";
    import { flip } from "svelte/animate";
    import PollStore from "../stores/PollStore.js";
    import PollDetails from "./PollDetails.svelte";

</script>

<div class="poll-list">
    <!-- $PollStore gets data from store -->
    {#each $PollStore as poll (poll.id)}
        <div in:fade animate:flip={{ duration: 500 }} class="poll-details-container">
            <PollDetails poll={poll} />
        </div>
    {/each}
</div>

<style>
    .poll-list {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        gap: 1rem 1.25rem;
    }
</style>