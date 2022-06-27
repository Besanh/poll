<script>
    import { createEventDispatcher } from "svelte";
    import Button from "../../src/shared/Button.svelte";

    const dispatch = createEventDispatcher();
    let customFields = { question: "", answerA: "", answerB: "" };
    let errorFields = { question: "", answerA: "", answerB: "" };
    let validValue = false;

    const submitHandler = () => {
        console.log(customFields);
        validValue = true;
        if (customFields.question.trim().length < 5) {
            validValue = false;
            errorFields.question =
                "Question must be at least 5 characters long";
        } else {
            errorFields.question = "";
        }
        if (customFields.answerA.trim().length < 1) {
            validValue = false;
            errorFields.answerA = "Answer A cannot be empty";
        } else {
            errorFields.answerA = "";
        }
        if (customFields.answerB.trim().length < 1) {
            validValue = false;
            errorFields.answerB = "Answer B cannot be empty";
        } else {
            errorFields.answerB = "";
        }

        if (validValue) {
            console.log("value", customFields);
            let poll = {
                ...customFields,
                voteA: 0,
                voteB: 0,
                id: Math.random(),
            };
            dispatch("submitPollForm", poll);
        }
    };
</script>

<form on:submit|preventDefault={submitHandler}>
    <div class="form-field">
        <label for="question">Question</label>
        <input type="text" id="question" bind:value={customFields.question} />
        <div class="error">{errorFields.question}</div>
    </div>
    <div class="form-field">
        <label for="answerA">Answer A</label>
        <input type="text" id="answerA" bind:value={customFields.answerA} />
        <div class="error">{errorFields.answerA}</div>
    </div>
    <div class="form-field">
        <label for="answerB">Answer B</label>
        <input type="text" id="answerB" bind:value={customFields.answerB} />
        <div class="error">{errorFields.answerB}</div>
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
    .error {
        font-weight: bold;
        font-size: 12px;
        color: #d91b42;
    }
</style>
