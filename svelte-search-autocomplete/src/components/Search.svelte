<script lang="ts">
    import axios, { AxiosResponse } from 'axios';
    import { onMount } from 'svelte';
    import SuggestionList from './SuggestionList.svelte';

    const API_URL: string = 'https://pokeapi.co/api/v2/pokemon';
    const MAX_POKEMON_LIMIT: number = 1000;

    export let pokemonDetails: any;

    let query: string = '';
    let suggestions: string[] = [];
    let showSuggestions: boolean = false;

    const fetchPokemonList = async (): Promise<string[]> => {
        try {
            const response: AxiosResponse = await axios.get(
                `${API_URL}?limit=${MAX_POKEMON_LIMIT}`
            );
            return response.data.results.map(
                (pokemon: { name: string }) => pokemon.name
            );
        } catch (error) {
            console.error('Error fetching data:', error);
            return [];
        }
    };

    const search = async (): Promise<void> => {
        query = query.trim().toLowerCase();
        if (query !== '') {
            suggestions = (await fetchPokemonList()).filter((pokemon: string) =>
                pokemon.startsWith(query)
            );
            showSuggestions = true;
        } else {
            suggestions = [];
            showSuggestions = false;
        }
    };

    const handleClickOutside = (event: MouseEvent): void => {
        const input: Element | null = document.querySelector('input');
        if (input && !input.contains(event.target as Node)) {
            showSuggestions = false;
        }
    };

    onMount(() => {
        document.addEventListener('click', handleClickOutside);
    });

    const handleSearch = (): void => {
        if (query.trim() !== '') {
            getPokemonDetails(query);
        }
    };

    const getPokemonDetails = async (name: string): Promise<void> => {
        try {
            const response: AxiosResponse = await axios.get(
                `${API_URL}/${name}`
            );
            pokemonDetails = response.data;
        } catch (error) {
            console.error('Error fetching Pokemon details:', error);
            pokemonDetails = null;
        }
    };

    const handleSuggestionClick = (suggestion: string): void => {
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

    <SuggestionList
        show={showSuggestions}
        {suggestions}
        {handleSuggestionClick}
    />
</div>
