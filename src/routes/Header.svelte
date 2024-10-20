<script lang="ts">
    let { 
        name 
    }: {
        name: string;
    } = $props();
</script>

<h1>Hello from {name}</h1>
<h2>{name.replace("y","z")}</h2>

<style>

</style>