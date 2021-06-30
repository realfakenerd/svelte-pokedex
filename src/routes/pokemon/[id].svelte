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
	export let order = pokeman.order;
</script>

<svelte:head>
	<title>{pokeman.name}</title>
	<link rel="icon" href={pokeman.sprites['front_default']} />
</svelte:head>
<h1 class="text-4xl text-center my-8 uppercase">{pokeman.name}</h1>
<div
	class="transition-shadow duration-300
			grid md:grid-rows-1 md:grid-cols-2 place-items-cente
			bg-gray-200 rounded-lg hover:shadow-lg main-img "
>
	<div class="container h-full w-full relative bg-gray-400 z-index-container md:rounded-l-lg overflow-hidden">
		<img src={imgSrc} alt={pokeman.name} />
		<img
			class="absolute z-index-glow inset-0 filter"
			src={imgSrc}
			alt={pokeman.name}
		/>
	</div>
	<ul class="grid md:grid-cols-2 place-items-center">
		<li>Type: <strong>{type}</strong></li>
		<li>Order: <strong>{order}</strong></li>
		<li>Height: <strong>{pokeman.height}</strong></li>
		<li>Weight: <strong>{pokeman.weight}</strong></li>
	</ul>
</div>

<style>
	.z-index-container {
		z-index: 10;
	}
	.z-index-glow {
		transition: filter 400ms linear;
		z-index: -1;
		filter: blur(6px) saturate(1.5)
	}
	
	.main-img:hover .z-index-glow {
		filter: blur(16px) saturate(3)
	}
</style>
