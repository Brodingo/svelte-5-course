<script lang="ts">
    let { 
        name,
        fake_name = 'Dingo'
    }: {
        name: string;
        fake_name?: string | null;
    } = $props();
</script>

<h1>Hello from {name}</h1>
<h2>{name.replaceAll("y","z")}</h2>

{fake_name}

<style>

</style>