<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();
    let customFields = { question: "", answerA: "", answerB: "" };
    const submitHandler = () => {
        console.log(customFields);
        // dispatch('submitPollForm', customFields)
    };
</script>

<form on:submit|preventDefault={submitHandler}>
    <div class="form-field">
        <label for="question">Poll question:</label>
        <input type="text" id="question" bind:value={customFields.question} />
    </div>
    <div class="form-field">
        <label for="answer-a">Answer A:</label>
        <input type="text" id="answer-a" bind:value={customFields.answerA} />
    </div>
    <div class="form-field">
        <label for="answer-b">Answer B:</label>
        <input type="text" id="anser-b" bind:value={customFields.answerB} />
    </div>
    <button type="submit">Send</button>
</form>

<style>
    form {
        width: 400px;
        margin: 0 auto;
        text-align: center;
    }
    .form-field {
        margin: 18px auto;
        text-align: left;
    }
    input {
        width: 100%;
        border-radius: 6px;
    }
    label {
        margin: 10px auto;
    }
</style>
