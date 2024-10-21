<script lang="ts">
    import Header from './Header.svelte'

    let formState = $state({
        answers: {},
        step: 0,
        error: ''
    });

    const QUESTIONS = [
        {
            question: "What is your name?",
            id: 'name',
            type: 'text'
        },
        {
            question: "What is your birthday?",
            id: 'birthday',
            type: 'date'

        },
        {
            question: "What's your favorite color",
            id: 'color',
            type: 'color'
        }
    ];

    function nextStep(id: string) {
        if (formState.answers[id]) {
            formState.step += 1;
            formState.error = "";
        } else {
            formState.error = "Please fill out the form input";
        }
    }

</script>

<Header name={formState.answers.name} />

<main>
    {#if formState.step >= QUESTIONS.length}
        <p>Thank you!</p>
    {/if}
    <p>Step: {formState.step + 1}</p>

    {#each QUESTIONS as question, index (question.id)}
        {#if formState.step === index}
        {@render formStep(question)}        
        {/if}
    {/each}

    {#if formState.error}
        <p class="error">{formState.error}</p>
    {/if}
</main>

{JSON.stringify(formState)}

{#snippet formStep({question, id, type} : {
    type: string; id: string; question: string;
})}
    <article>
        <div>
            <label for="{id}">{question}</label>
            <input {type} {id} bind:value={formState.answers[id]}>
        </div>
        <button onclick="{() => nextStep(id)}">Next</button>
    </article>
{/snippet}

<style>
    :global(body) {
        background-color: #222;
        color: #eee;
    }
    :global(div) {
        background-color: slategray;
    }
    .error {
        color: red;
    }
</style>