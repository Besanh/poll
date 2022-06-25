<script>
    import { createEventDispatcher } from "svelte";
    import Button from "../../src/shared/Button.svelte";

    const dispatch = createEventDispatcher();
    let customFields = { question: "", answerA: "", answerB: "" };
    const submitHandler = () => {
        console.log(customFields);
        // dispatch('submitPollForm', customFields)
    };
</script>

<form on:submit|preventDefault={submitHandler}>
    <div class="form-field">
        <label for="question">Question</label>
        <input type="text" id="question" bind:value={customFields.question} />
    </div>
    <div class="form-field">
        <label for="answerA">Answer A</label>
        <input type="text" id="answerA" bind:value={customFields.answerA} />
    </div>
    <div class="form-field">
        <label for="answerB">Answer B</label>
        <input type="text" id="answerB" bind:value={customFields.answerB} />
    </div>
    <Button type_btn="secondary" flat={true} inverse={true}>Add</Button>
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
