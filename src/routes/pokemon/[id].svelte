<script context="module">
	export async function load({ params }) {
		const id = params.id;
		const url = `https://pokeapi.co/api/v2/pokemon/${id}`;
		const res = await fetch(url);
		const pokeman = await res.json();

		const urlDesc = `https://pokeapi.co/api/v2/pokemon-species/${id}/`;
		const pokemanSpecies = await (await fetch(urlDesc)).json();
		return { props: { pokeman, pokemanSpecies } };
	}
</script>

<script>
	import { fade } from 'svelte/transition';

	export let pokeman;
	export let pokemanSpecies;

	let title;
	$: {
		title = pokeman.name.charAt(0).toUpperCase() + pokeman.name.slice(1);
	}
</script>

<svelte:head>
	<title>{title} | Pokedex</title>
</svelte:head>

<div class="flex items-center justify-between mt-10">
	<a
		class="bg-gray-300 w-full rounded-l-md text-center py-3 px-2 mr-1 hover:bg-cyan-500 duration-150"
		href={pokeman.id - 1 === 0 ? `/` : `/pokemon/${pokeman.id - 1}`}>Previous Pokemon</a
	>

	<a
		class="bg-gray-300 w-full rounded-r-md text-center py-3 px-2 hover:bg-cyan-500 duration-150"
		href={`/pokemon/${pokeman.id + 1}`}>Next Pokemon</a
	>
</div>
<div class="flex flex-col items-center">
	<h1 class="text-4xl text-center my-8 uppercase" transition:fade>
		{pokeman.name} <span class="text-slate-500 ml-2">#{pokeman.id}</span>
	</h1>
</div>

<div
	class="grid gap-4 md:grid-cols-2 grid-cols-1 rounded-lg bg-slate-100 p-5 pb-20 w-fit sm:mx-auto"
	transition:fade
>
	<div class="flex flex-col items-center ">
		<img
			class="card-image bg-slate-200 rounded-md w-full mb-4 hover:scale-105 duration-300"
			src={pokeman.sprites.other['official-artwork'].front_default}
			alt={pokeman.name}
		/>
		<div class="p-6 bg-slate-400 w-full rounded-md hover:scale-105 duration-300">
			<h2
				class="mb-2 text-lg text-slate-800 underline decoration-slate-800 underline-offset-1 uppercase subpixel-antialiased font-semibold"
			>
				Stats:
			</h2>
			{#each pokeman.stats as stats}
				<p>
					<span class="font-semibold">
						{stats.stat.name.charAt(0).toUpperCase() + stats.stat.name.slice(1)}:
					</span>
					{stats.base_stat}
				</p>
			{/each}
		</div>
	</div>
	<div>
		<div
			class="p-6 bg-cyan-500 w-full rounded-md grid grid-cols-2 mb-7 hover:scale-105 duration-300"
		>
			<p class="flex flex-col text-white mb-3">
				Height
				<span class="text-black mt-1 text-lg">{Math.floor(pokeman.height * 3.937)} in</span>
			</p>
			<p class="flex flex-col text-white mb-3">
				Weight
				<span class="text-black mt-1 text-lg"
					>{Math.floor((pokeman.weight / 10) * 2.20462)} lbs</span
				>
			</p>
			<p class="flex flex-col text-white mb-3">
				Color
				<span class="text-black mt-1 text-lg"
					>{pokemanSpecies.color.name.charAt(0).toUpperCase() +
						pokemanSpecies.color.name.slice(1)}</span
				>
			</p>
			<p class="flex flex-col text-white mb-3">
				Habitat
				<span class="text-black mt-1 text-lg"
					>{pokemanSpecies.habitat.name.charAt(0).toUpperCase() +
						pokemanSpecies.habitat.name.slice(1)}</span
				>
			</p>
			<p class="flex flex-col text-white mb-3">
				Abilities
				<span class="text-black mt-1 text-lg"
					>{pokeman.abilities[0].ability.name.charAt(0).toUpperCase() +
						pokeman.abilities[0].ability.name.slice(1)}</span
				>
			</p>
		</div>
		<h2 class="font-semibold text-lg mb-7">Type</h2>
		<div class="flex">
			{#each pokeman.types as type}
				<p
					class="bg-slate-400 rounded px-9 py-1 w-32 mx-2 text-center hover:scale-105 duration-300"
				>
					{type.type.name.charAt(0).toUpperCase() + type.type.name.slice(1)}
				</p>
			{/each}
		</div>
	</div>
</div>
