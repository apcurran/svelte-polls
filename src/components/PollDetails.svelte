<script>
    import PollStore from "../stores/PollStore.js";
    import Button from "../shared/Button.svelte";
    import { tweened } from "svelte/motion";
    export let poll;

    // Reactive value
    $: totalVotes = poll.votesA + poll.votesB;
    $: percentA = Math.floor(100 / totalVotes * poll.votesA) || 0;
    $: percentB = Math.floor(100 / totalVotes * poll.votesB) || 0;

    // Tweened percentages for bars
    const tweenedA = tweened(0);
    const tweenedB = tweened(0);
    $: tweenedA.set(percentA);
    $: tweenedB.set(percentB);

    function handleVote(option, id) {
        PollStore.update(currentPolls => {
            let copiedPolls = [...currentPolls];
            let upvotedPoll = copiedPolls.find(poll => poll.id === id);
    
            if (option === "a") {
                upvotedPoll.votesA++;
            } else if (option === "b") {
                upvotedPoll.votesB++;
            }
    
            return copiedPolls;
        });
    }

    function handleDelete(id) {
        PollStore.update(currentPolls => {
            return currentPolls.filter(poll => poll.id !== id);
        });
    }
</script>

<div class="poll">
    <h3>{poll.question}</h3>
    <p>Total votes: {totalVotes}</p>
    <div on:click={() => handleVote("a", poll.id)} class="poll__answer-group">
        <div style="width: {$tweenedA}%" class="percent percent-a"></div>
        <span class="poll__answer poll__answer__answer-a">{poll.answerA} ({poll.votesA})</span>
    </div>
    <div on:click={() => handleVote("b", poll.id)}  class="poll__answer-group">
        <div style="width: {$tweenedB}%" class="percent percent-b"></div>
        <span class="poll__answer poll__answer__answer-b">{poll.answerB} ({poll.votesB})</span>
    </div>
    <Button flat={true} on:click={() => handleDelete(poll.id)}>Delete</Button>
</div>

<style>
    .poll {
        padding: 1.35rem;
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

    .percent {
        height: 100%;
        position: absolute;
        
    }

    .percent-a {
        border-left: 4px solid #d91b42;
        background-color: rgba(217, 27, 66, .2);
    }

    .percent-b {
        border-left: 4px solid #45c496;
        background-color: rgba(69, 196, 150, .2);
    }

</style>