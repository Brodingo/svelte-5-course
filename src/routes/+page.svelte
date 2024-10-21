<script lang="ts">
    import Header from './Header.svelte'
    let name = $state('Brody');
    let status: 'OPEN' | 'CLOSED' = $state('OPEN');
    let full_name = $derived(name + " " + 'Kwiatkowski')

    // function toggle() {
    //     status = status == 'OPEN' ? 'CLOSED' : 'OPEN'
    // }
    function onclick() {
        status = status == 'OPEN' ? 'CLOSED' : 'OPEN';
    }
</script>

<Header {name} />

<h3>{full_name}</h3>

<input type="text" bind:value={name} />

<p>The store is now {status}</p>

<!-- <button {onclick}>Toggle Status</button> -->
<button onclick={() => {
    status = status == 'OPEN' ? 'CLOSED' : 'OPEN';
}}>Toggle Status</button>