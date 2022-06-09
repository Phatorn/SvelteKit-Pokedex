<script lang="ts" context="module">
	export async function load(num: number) {
		const url = `https://pokeapi.co/api/v2/pokemon?limit=${num}`;
		const res = await fetch(url);
		const data = await res.json();
		const loadedPokemon = data.results.map((data: any, index: number) => {
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

<script lang="ts">
	//import type {Pokeman} from "../types/pokeman"
	//import { each } from "svelte/internal"
	//import {pokemon} from "../stores/pokestore"
	import PokemanCard from "../components/pokemanCard.svelte"
	export let pokemon: any
	//console.log($pokemon)
	let searchTerm = '';
	let filteredPokemon: any = [];

	$: {
		//console.log(searchTerm)
		if (searchTerm) {
			filteredPokemon = pokemon.filter((pokeman: any) =>
				pokeman.name.toLowerCase().includes(searchTerm.toLowerCase())
			);
		} else {
			filteredPokemon = [...pokemon];
		}
	}
</script>

<svelte:head>
	<title>Svelte Kit Pokedex</title>
</svelte:head>
<h1 class="text-4xl text-center my-8 uppercase">Svelte Kit Pokedex</h1>

<input
	class="w-full rounded-md text-lg p-4 border-2 border-gray-200"
	type="text"
	bind:value={searchTerm}
	placeholder="Search Pokemon"
/>

<div class="py-4 grid gap-4 md:grid-cols-2 grid-cols-1">
	{#each filteredPokemon as pokeman}
		<PokemanCard {pokeman} />
	{/each}
</div>
