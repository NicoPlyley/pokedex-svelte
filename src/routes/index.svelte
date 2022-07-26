<script>
  import { pokemon } from '../stores/pokestore';
  import PokemanCard from '../components/pokemanCard.svelte'

  let searchTerm = "";
  let filteredPokemon;
  let noPokemon = false

  $: {
    if (searchTerm) {
      filteredPokemon = $pokemon.filter((pokeman) => pokeman.name.toLowerCase().includes(searchTerm.toLowerCase()));
      noPokemon = filteredPokemon.length === 0;
    } else {
      filteredPokemon = [...$pokemon]
    }
  }
</script>

<svelte:head>
  <title>Pokedex - Svelte Kit</title>
</svelte:head>

<h1 class="text-4xl text-center my-8">Svelte Kit Pokédex</h1>

<input
    bind:value={searchTerm}
    class="w-full rounded-md text-lg p-4 border-2 border-gray-200"
    type="text"
    placeholder="Search Pokémon"
>

<div class="py-4 grid gap-4 md:grid-cols-2 grid-cols-1">
  {#if !noPokemon}
    {#each filteredPokemon as pokeman}
      <PokemanCard pokeman={pokeman} />
    {/each}
  {:else}
    <p class="text-lg">No Pokémon found 😔</p>
  {/if}
</div>
