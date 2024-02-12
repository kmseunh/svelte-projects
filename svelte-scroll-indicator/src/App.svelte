<script lang="ts">
    import axios from 'axios';
    import { onMount } from 'svelte';
    import ScrollIndicator from './components/ScrollIndicator.svelte';

    interface Spell {
        id: string;
        name: string;
        description: string;
    }

    let spells: Spell[] = [];

    const fetchData = async () => {
        try {
            const response = await axios.get<Spell[]>(
                'https://hp-api.onrender.com/api/spells'
            );
            spells = response.data;
        } catch (error) {
            console.log('Error fetching data:', error);
        }
    };

    onMount(fetchData);
</script>

<div
    class="flex justify-center items-center min-h-screen bg-gray-800 text-white"
>
    <div class="max-w-4xl mx-auto px-4">
        <h1 class="text-4xl font-bold text-center mt-10 mb-8">
            🧙‍♂️ Harry Potter's Spells 🧙‍♀️
        </h1>
        <ScrollIndicator />
        <div class="grid grid-cols-1 gap-6">
            {#each spells as spell}
                <div class="bg-gray-900 rounded-lg p-6">
                    <h2 class="text-2xl font-semibold mb-2 text-yellow-400">
                        {spell.name}
                    </h2>
                    <p class="text-gray-300">{spell.description}</p>
                </div>
            {/each}
        </div>
    </div>
</div>
