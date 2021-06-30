<script context="module">
	export async function load({ page }) {
		const id = page.params.id;
		const url = `https://pokeapi.co/api/v2/pokemon/${id}`;
		const res = await fetch(url);
		const pokeman = await res.json();
		return { props: { pokeman } };
	}
</script>

<script>
	export let pokeman;
	export let type = pokeman.types[0].type.name;
	export let imgSrc = pokeman.sprites.other['official-artwork']['front_default'];
</script>

<svelte:head>
	<title>{pokeman.name}</title>
	<link rel="icon" href={pokeman.sprites['front_default']} />
</svelte:head>
<h1 class="text-4xl text-center my-8 uppercase">{pokeman.name}</h1>
<div class="grid grid-rows-1 grid-cols-2">
	<ul>
		<li>Type: <strong>{type}</strong></li>
		<li>Height: <strong>{pokeman.height}</strong></li>
		<li>Weight: <strong>{pokeman.weight}</strong></li>
	</ul>
	<div class="container object-center h-full w-full relative mx-auto">
		<img class="" src={imgSrc} alt={pokeman.name} />
		<img class="absolute z-0 inset-0 filter blur-lg saturate-200" src={imgSrc} alt={pokeman.name} />
	</div>
</div>

<style>
	.z-0 {
		z-index: -1;
	}
</style>
