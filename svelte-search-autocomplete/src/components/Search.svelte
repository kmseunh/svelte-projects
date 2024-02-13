<script>
    import axios from 'axios';
    import { onMount } from 'svelte';

    const API_URL = 'https://pokeapi.co/api/v2/pokemon';
    const MAX_POKEMON_LIMIT = 1000;

    export let pokemonDetails;

    let query = '';
    let suggestions = [];
    let showSuggestions = false;

    const fetchPokemonList = async () => {
        try {
            const response = await axios.get(
                `${API_URL}?limit=${MAX_POKEMON_LIMIT}`
            );
            return response.data.results.map((pokemon) => pokemon.name);
        } catch (error) {
            console.error('Error fetching data:', error);
            return [];
        }
    };

    const search = async () => {
        query = query.trim().toLowerCase();
        if (query !== '') {
            suggestions = (await fetchPokemonList()).filter((pokemon) =>
                pokemon.startsWith(query)
            );
            showSuggestions = true;
        } else {
            suggestions = [];
            showSuggestions = false;
        }
    };

    const handleClickOutside = (event) => {
        const input = document.querySelector('input');
        if (input && !input.contains(event.target)) {
            showSuggestions = false;
        }
    };

    onMount(() => {
        document.addEventListener('click', handleClickOutside);
    });

    const handleSearch = () => {
        if (query.trim() !== '') {
            getPokemonDetails(query);
        }
    };

    const getPokemonDetails = async (name) => {
        try {
            const response = await axios.get(`${API_URL}/${name}`);
            pokemonDetails = response.data;
        } catch (error) {
            console.error('Error fetching Pokemon details:', error);
            pokemonDetails = null;
        }
    };

    const handleSuggestionClick = (suggestion) => {
        query = suggestion;
        showSuggestions = false;
        getPokemonDetails(query);
    };
</script>

<div class="relative">
    <input
        type="text"
        class="border border-gray-300 rounded-md px-4 py-2 w-64 shadow-sm focus:outline-none focus:ring focus:ring-blue-200"
        bind:value={query}
        on:input={search}
        placeholder="Enter Pokémon name"
    />
    <button
        class="ml-2 px-4 py-2 bg-blue-500 text-white rounded-md"
        on:click={handleSearch}>Search</button
    >

    {#if showSuggestions && suggestions.length > 0}
        <ul
            class="absolute w-64 mt-2 overflow-y-auto max-h-48 bg-white border border-gray-200 rounded-md shadow-md z-20"
        >
            {#each suggestions as suggestion}
                <li
                    class="cursor-pointer py-2 px-4 hover:bg-gray-100"
                    on:click={() => handleSuggestionClick(suggestion)}
                >
                    {suggestion}
                </li>
            {/each}
        </ul>
    {/if}
</div>

{#if pokemonDetails}
    <div class="mt-8 flex flex-col items-center">
        <div class="bg-gray-100 p-4 rounded-lg shadow-md">
            <h2 class="text-2xl font-bold mb-4">{pokemonDetails.name}</h2>
            <img
                src={pokemonDetails.sprites.front_default}
                alt={pokemonDetails.name}
                class="w-40 h-40 mb-4"
            />
            <p class="text-lg">Height: {pokemonDetails.height}</p>
            <p class="text-lg">Weight: {pokemonDetails.weight}</p>
        </div>
    </div>
{/if}
