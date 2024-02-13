<script>
    export let pokemonDetails;
</script>

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
