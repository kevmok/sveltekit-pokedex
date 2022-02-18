# Pokedex Built with SvelteKit

Pokedex svelte app that uses the PokeAPI to fetch the original 150 Pokemon. The use SvelteKit and dynamic routing makes this app quick and seamless to the user.

There's also a small built-in API, which is redundant but shows how to make an API from another API.

## Overview

### The Goal

User should be able to:

- [x] See a list of the original 150 Pokemon
- [x] Click on desired Pokemon to see its details
- [x] Search through the Pokedex for a specific Pokemon
- [x] Go to the next/previous Pokemon in the Pokemon Page

### Demo

[Website Demo](https://sveltekit-pokedex-rose.vercel.app/)

## Screenshots

![App Screenshot](https://i.imgur.com/QyNxPbZ.png)
![App Screenshot](https://i.imgur.com/VyTX2Hc.png)

## My process

### Built with

- Svelte Kit
- HTML
- Javascript
- Tailwind CSS

### What I learned

- Fetch an API at page load
- Svelte Layout
- Using Svelte:head for different page titles on dynamic routing
- Manipulating objects coming from an API
- Tailwind CSS
- How to make a simple search filter
- Dynamic Routing

```jsx
// At page load fetch API and return data response as props
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
// To use props from load
export let pokeman;
export let pokemanSpecies;
</script>
```

## Installation

Clone this repository and install the dependencies...

```bash
  git clone https://github.com/kevmok/sveltekit-pokedex.git my-app
  cd my-app
  npm install
```

```bash
  npm run dev
```

## Author

- Website - [kevinmok.com](https://kevinmok.com)
- GitHub - [@kevmok](https://www.github.com/Kevmok)
- Twitter - [@hustlerBoxer](https://twitter.com/hustlerBoxer)

## Acknowledgements

- [JamesQQuick](https://www.youtube.com/c/JamesQQuick) - For his amazing SvelteKit resources
- [PokeAPI](https://pokeapi.co/) - For their awesome meme API
