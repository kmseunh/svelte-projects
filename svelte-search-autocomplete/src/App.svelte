<script lang="ts">
    import axios, { AxiosResponse } from 'axios';
    import Search from './components/Search.svelte';
    import PokemonDetails from './components/PokemonDetails.svelte';

    const API_URL: string = 'https://pokeapi.co/api/v2/pokemon';
    const MAX_POKEMON_LIMIT: number = 1000;

    let pokemonDetails: any;

    const fetchPokemonDetails = async (name: string): Promise<void> => {
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

    const handleSearch = async (query: string): Promise<void> => {
        if (query.trim() !== '') {
            await fetchPokemonDetails(query);
        }
    };
</script>

<div class="flex flex-col items-center justify-center h-screen">
    <h1 class="text-4xl font-bold my-4 text-center">Pokémon Search</h1>

    <Search on:search={handleSearch} bind:pokemonDetails />

    <PokemonDetails {pokemonDetails} />
</div>
