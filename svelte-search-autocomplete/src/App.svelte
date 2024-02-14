<script lang="ts">
    import Search from './components/Search.svelte';
    import PokemonDetails from './components/PokemonDetails.svelte';

    let pokemonDetails: any;
</script>

<div class="flex flex-col items-center justify-center h-screen">
    <h1 class="text-4xl font-bold my-4 text-center">Pokémon Search</h1>

    <Search bind:pokemonDetails />

    <PokemonDetails {pokemonDetails} />
</div>
