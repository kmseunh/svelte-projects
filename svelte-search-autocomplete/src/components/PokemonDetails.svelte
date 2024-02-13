<script lang="ts">
    export let pokemonDetails: any; // 이 부분에서 any 대신에 실제 PokemonDetails의 타입을 사용하는 것이 좋습니다.
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
