<script>
    import { onMount } from 'svelte';
    import axios from 'axios';
    import PokemonDetails from './components/PokemonDetails.svelte';
    import Search from './components/Search.svelte';
    import SuggestionList from './components/SuggestionList.svelte';

    const API_URL = 'https://pokeapi.co/api/v2/pokemon';
    const MAX_POKEMON_LIMIT = 1000;

    let query = '';
    let suggestions = [];
    let selectedPokemon = null;
    let pokemonDetails = null;
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

    const fetchPokemonDetails = async (name) => {
        try {
            const response = await axios.get(`${API_URL}/${name}`);
            pokemonDetails = response.data;
        } catch (error) {
            console.error('Error fetching Pokemon details:', error);
            pokemonDetails = null;
        }
    };

    const handleSearch = () => {
        if (query.trim() !== '') {
            getPokemonDetails(query);
        }
    };

    const getPokemonDetails = async (name) => {
        await fetchPokemonDetails(name);
    };

    const handleSuggestionClick = (suggestion) => {
        query = suggestion;
        selectedPokemon = suggestion;
        getPokemonDetails(selectedPokemon);
        showSuggestions = false;
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
</script>

<div class="flex flex-col items-center justify-center h-screen">
    <h1 class="text-4xl font-bold my-4 text-center">Pokémon Search</h1>

    <div class="relative">
        <Search bind:query on:input={search} on:search={handleSearch} />
        <SuggestionList
            {suggestions}
            {showSuggestions}
            onSuggestionClick={handleSuggestionClick}
        />
    </div>

    <PokemonDetails {pokemonDetails} />
</div>
