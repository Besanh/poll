<script>
    import { createEventDispatcher } from "svelte";
    import Card from "../shared/Card.svelte";
    import PollStore from "../../src/stores/PollStore";

    const dispatch = createEventDispatcher();
    // let poll;
    $: total_vote = poll.voteA + poll.voteB;
    $: percentA = Math.floor((100 / total_vote) * poll.voteA);
    $: percentB = Math.floor((100 / total_vote) * poll.voteB);

    const handleVote = (option, id) => {
        PollStore.update((current_poll) => {
            let copiedPoll = [...current_poll];
            let updatePoll = copiedPoll.find((poll) => poll.id == id);
            if (option === "a") {
                updatePoll.voteA++;
            } else {
                updatePoll.voteB++;
            }
            return copiedPoll
        });
    };

    export let poll;
</script>

<Card>
    <div class="poll-detail">
        <h3>{poll.question}</h3>
        <p>Total Vote: {total_vote}</p>
        <div class="answer" on:click={() => handleVote("a", poll.id)}>
            <div class="percent percent-a" style:width="{percentA}%" />
            <span>{poll.answerA} ({poll.voteA})</span>
        </div>
        <div class="answer" on:click={() => handleVote("b", poll.id)}>
            <div class="percent percent-b" style:width="{percentB}%" />
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
    .percent {
        height: 100%;
        position: absolute;
        box-sizing: border-box;
    }
    .percent-a {
        border-left: 4px solid #d91b42;
        background: rgba(217, 27, 66, 0.2);
    }
    .percent-b {
        border-left: 4px solid #45c496;
        background: rgba(69, 196, 150, 0.2);
    }
</style>
