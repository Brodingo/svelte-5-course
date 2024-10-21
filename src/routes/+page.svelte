<script lang="ts">
    import Header from './Header.svelte'

    let formState = $state({
        name: '',
        birthday: '',
        step: 0,
        error: ''
    });

</script>

<Header name={formState.name} />

<main>
    <p>Step: {formState.step + 1}</p>

    {@render formStep({
        question: "What's your name",
        id: 'name',
        type: 'text'
    })}
</main>

{#snippet formStep({question, id, type} : {
    type: string; id: string; question: string;
})}
    <article>
        <div>
            <label for="{id}">{question}</label>
            <input {type} {id} bind:value={formState[id]}>
        </div>
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