<script>
	import { pokemon } from '../stores/pokestore';
	console.log($pokemon);
</script>

<svelte:head>
	<title>Pokedex</title>
</svelte:head>

<h1>Wellcome to the Pokedex</h1>

<div class="grid">
    {#each $pokemon as pokeman}
        <h3>{pokeman.name}</h3>
    {/each}
</div>

<style>
    .grid {
        display: grid;
        grid-template-columns: auto auto auto auto auto;
        place-items: center;
        color: red
    }
</style>