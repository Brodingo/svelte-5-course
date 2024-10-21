<script lang="ts">
	import { fly } from 'svelte/transition';
    import Header from './Header.svelte'

    let formState = $state({
        answers: {},
        step: 0,
        error: ''
    });

    $inspect(formState.step);

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

    // Will run onMount        
    // $effect(() => {
    //     console.log("on mounted");
    //     // Will run when unmounted or destroyed
    //     // Before effect Re-runs
    //     return () => {
    //         console.log("on unmounted");
    //     }
    // });

    // Svelte knows to re-run because its using compiled with the formState.step var
    // $effect(() => {
    //     // This will re-run when formState.step has changed
    //     console.log('formState', formState.step)
    //     // DONT create state based on other state, in effect
    //     // use $derived() !!!
    //     return () => {
    //         // before effect re-runs
    //         console.log('before formState reruns', formState.step);
    //     }
    // });

</script>

<Header name={formState.answers.name} />

<main>
    {#if formState.step >= QUESTIONS.length}
        <p>Thank you!</p>
    {/if}
    <p>Step: {formState.step + 1}</p>

    {#each QUESTIONS as question, index (question.id)}
        {#if formState.step === index}
        <div 
            in:fly={{x: 200, duration: 200, opacity: 0, delay: 200}}
            out:fly={{x: -200, duration: 200, opacity: 0}}
            >
            {@render formStep(question)}        
        </div>
        {/if}
    {/each}

    {#if formState.error}
        <p class="error">{formState.error}</p>
    {/if}
</main>

<!-- {JSON.stringify(formState)} -->

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