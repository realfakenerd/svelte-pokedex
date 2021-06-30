<script>
	import { pokemon } from '../stores/pokestore';
	import PokemanCard from '../components/pokemanCard.svelte';

	let searchTerm = '';
	let filteredPokemon = [];
	$: {
		console.log(searchTerm);
		if (searchTerm) {
			filteredPokemon = $pokemon.filter((pokeman) =>
				pokeman.name.toLowerCase().includes(searchTerm.toLocaleLowerCase())
			);
		} else {
			filteredPokemon = [...$pokemon];
		}
	}
</script>

<svelte:head>
	<title>Pokedex</title>
</svelte:head>

<h1 class="text-4xl text-center my-8 uppercase">Wellcome to the amazing Pokedex</h1>

<input
	class="w-full focus:border-4 rounded-md text-lg p-5 border-2 border-gray-200"
	type="text"
	placeholder="Search Pokemon"
	bind:value={searchTerm}
/>

<div class="py-4 grid gap-4 md:grid-cols-2 grid-cols-1">
	{#each filteredPokemon as pokeman}
		<PokemanCard {pokeman} />
	{/each}
</div>
