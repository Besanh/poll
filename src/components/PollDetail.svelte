<script>
    import { createEventDispatcher } from "svelte";
    import Card from "../shared/Card.svelte";

    const dispatch = createEventDispatcher();
    // let poll;
    $: total_vote = poll.voteA + poll.voteB;

    const handleVote = (option, id) => {
        dispatch("vote", { option, id });
    };

    export let poll;
</script>

<Card>
    <div class="poll-detail">
        <h3>{poll.question}</h3>
        <p>Total Vote: {total_vote}</p>
        <div class="answer" on:click={() => handleVote("a", poll.id)}>
            <div class="percent percent-a" />
            <span>{poll.answerA} ({poll.voteA})</span>
        </div>
        <div class="answer" on:click={() => handleVote("b", poll.id)}>
            <div class="percent percent-b" />
            <span>{poll.answerB} ({poll.voteB})</span>
        </div>
    </div>
</Card>

<style>
    h3 {
        margin: 0 auto;
        color: #555;
    }
    p {
        margin-top: 6px;
        font-size: 14px;
        color: #aaa;
        margin-bottom: 30px;
    }
    .answer {
        background: #fafafa;
        cursor: pointer;
        margin: 10px auto;
        position: relative;
    }
    .answer:hover {
        opacity: 0.6;
    }
    span {
        display: inline-block;
        padding: 10px 20px;
    }
</style>
