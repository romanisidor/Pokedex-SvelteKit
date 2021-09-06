<script context="module">
	//Esta función permite hacer uso del SSR (Server Side Rendering)
	//Su propósito es cargar la data desde el servidor antes de que el usuario (cliente) haga una petición del servidor
	export async function load({ page }) {
		const url = `https://pokeapi.co/api/v2/pokemon?limit=150`;
		const res = await fetch(url);
		const data = await res.json();
		const loadedPokemon = data.results.map((data, index) => {
			return {
				name: data.name,
				id: index + 1,
				image: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${
					index + 1
				}.png`
			};
		});
		return { props: { pokemon: loadedPokemon } };
	}
</script>

<script>
	import PokemanCards from '../components/pokemanCards.svelte';

	export let pokemon;
  
	let searchWord = '';

	let filteredPokemon = [];

	$: {
		if (searchWord) {
			//Busca el pokemon
			filteredPokemon = pokemon.filter((pokeman) =>
				pokeman.name.toLowerCase().includes(searchWord.toLowerCase())
			);
		} else {
			filteredPokemon = [...pokemon];
		}
	}
</script>

<svelte:head>
	<title>Pokedex App</title>
</svelte:head>

<h1 class="text-4xl text-center my-8 uppercase">SvelteKit Pokedex</h1>

<input
	type="text"
	class="w-full rounded-md text-lg p-4 border-2 border-gray-200"
	placeholder="Buscar el pokemón..."
	bind:value={searchWord}
/>

<!--Por medio de los props le paso la información obtenida del fetch-->
<div class="py-4 grid gap-4 grid-cols-1 md:grid-cols-2">
	{#each filteredPokemon as pokeman}
		<PokemanCards {pokeman} />
	{/each}
</div>

<style>
</style>
