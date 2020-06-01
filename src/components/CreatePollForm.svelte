<script>
    import { createEventDispatcher } from "svelte";
    import Button from "../shared/Button.svelte";

    let dispatch = createEventDispatcher();

    let fields = {
        question: "",
        answerA: "",
        answerB: ""
    };

    let errors = {
        question: "",
        answerA: "",
        answerB: ""
    };

    let valid = false;

    function handleSubmit() {
        valid = true;
        // Validate
        if (fields.question.trim().length < 5) {
            valid = false;
            errors.question = "Question must be at least 5 characters long.";
        } else {
            // Clear error
            errors.question = "";
        }

        // Validate
        if (fields.answerA.trim().length < 1) {
            valid = false;
            errors.answerA = "Answer A cannot be empty.";
        } else {
            // Clear error
            errors.answerA = "";
        }

        // Validate
        if (fields.answerB.trim().length < 1) {
            valid = false;
            errors.answerB = "Answer B cannot be empty.";
        } else {
            // Clear error
            errors.answerB = "";
        }

        // Add new poll
        if (valid) {
            let poll = { ...fields, votesA: 0, votesB: 0, id: Date.now().toString() }
            
            dispatch("add", poll);
        }
    }
</script>

<form on:submit|preventDefault={handleSubmit}>
    <div class="form-group">
        <label for="question">Poll Question</label>
        <input bind:value={fields.question} type="text" id="question" name="question">
        <p class="error">{errors.question}</p>
    </div>
    <div class="form-group">
        <label for="answer-a">Answer A:</label>
        <input bind:value={fields.answerA} type="text" id="answer-a" name="answer-a">
        <p class="error">{errors.answerA}</p>
    </div>
    <div class="form-group">
        <label for="answer-b">Answer B:</label>
        <input bind:value={fields.answerB} type="text" id="answer-b" name="answer-b">
        <p class="error">{errors.answerB}</p>
    </div>
    <Button type={"secondary"} flat={true}>Add Poll</Button>
</form>

<style>
    form {
        width: 35rem;
        margin: 0 auto;
    }

    .form-group {
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        margin-bottom: 1.25rem;
    }

    input {
        width: 100%;
        border: 1px solid #ddd;
        padding: .5rem;
        border-radius: 4px;
    }

    label {
        margin-bottom: .5rem;
    }

    .error {
        font-weight: bold;
        color: darkred;
        font-size: .95rem;
    }
</style>