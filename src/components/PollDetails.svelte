<script>
    import { createEventDispatcher } from "svelte";
    export let poll;

    const dispatch = createEventDispatcher();

    // Reactive value
    $: totalVotes = poll.votesA + poll.votesB;

    function handleVote(option, id) {
        dispatch("vote", { option, id });
    }
</script>

<div class="poll">
    <h3>{poll.question}</h3>
    <p>Total votes: {totalVotes}</p>
    <div on:click={() => handleVote("a", poll.id)} class="poll__answer-group">
        <div class="percent percent-a"></div>
        <span class="poll__answer poll__answer__answer-a">{poll.answerA} ({poll.votesA})</span>
    </div>
    <div on:click={() => handleVote("b", poll.id)}  class="poll__answer-group">
        <div class="percent percent-b"></div>
        <span class="poll__answer poll__answer__answer-b">{poll.answerB} ({poll.votesB})</span>
    </div>
</div>

<style>
    .poll {
        padding: 1.25rem;
        border-radius: 10px;
        box-shadow: 0 2px 6px rgba(0, 0, 0, .2);
    }

    h3 {
        color: #444;
    }

    p {
        margin-bottom: 2rem;
        font-size: .95rem;
        color: #888;
    }

    .poll__answer-group {
        position: relative;
        margin: 1rem auto;
        background-color: #f2f2f2;
        cursor: pointer;
    }

    .poll__answer-group:hover {
        opacity: .6;
    }

    span {
        display: inline-block;
        padding: .7rem 1.5rem;
    }

</style>