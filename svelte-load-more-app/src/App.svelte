<script lang="ts">
    import { onMount } from 'svelte';
    import { writable } from 'svelte/store';

    interface Post {
        userId: number;
        id: number;
        title: string;
        body: string;
    }

    let items = writable<Post[]>([]);
    let isLoading = false;

    const fetchData = async () => {
        try {
            isLoading = true;
            const response = await fetch(
                'https://jsonplaceholder.typicode.com/posts'
            );
            const data = await response.json();
            items.update((_) => data.slice(0, 9));
        } catch (error) {
            console.error('Error fetching data:', error);
        } finally {
            isLoading = false;
        }
    };

    onMount(fetchData);

    const loadMore = async () => {
        try {
            isLoading = true;
            if ($items.length > 0) {
                const lastItemId = $items[$items.length - 1].id;

                const response = await fetch(
                    `https://jsonplaceholder.typicode.com/posts?_start=${
                        lastItemId + 1
                    }&_limit=9`
                );
                const data = await response.json();
                items.update((existingItems) => [...existingItems, ...data]);
            }
        } catch (error) {
            console.error('Error fetching data:', error);
        } finally {
            isLoading = false;
        }
    };
</script>

<div class="flex flex-col justify-center items-center m-8">
    <h1 class="mb-4 text-4xl">Load More App</h1>
    <div
        class="max-w-screen-xl mx-auto grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4"
    >
        {#each $items as item}
            <div class="bg-white shadow-lg rounded-lg overflow-hidden">
                <div class="p-6">
                    <h2 class="text-xl font-semibold mb-2">{item.title}</h2>
                    <p class="text-gray-700">{item.body}</p>
                </div>
            </div>
        {/each}
    </div>
    <button
        class="mt-4 px-4 py-2 bg-blue-500 text-white rounded"
        on:click={loadMore}
        disabled={isLoading}
    >
        {#if isLoading}
            <div class="loader"></div>
        {:else}
            Load More
        {/if}
    </button>
</div>

<style>
    .loader {
        border: 4px solid #f3f3f3;
        border-top: 4px solid #3498db;
        border-radius: 50%;
        width: 20px;
        height: 20px;
        animation: spin 2s linear infinite;
        margin: auto;
    }

    @keyframes spin {
        0% {
            transform: rotate(0deg);
        }
        100% {
            transform: rotate(360deg);
        }
    }
</style>
