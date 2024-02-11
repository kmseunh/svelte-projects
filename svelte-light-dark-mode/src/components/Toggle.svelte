<script lang="ts">
    import { createEventDispatcher, onMount } from 'svelte';

    let darkMode: boolean = false;
    const dispatch = createEventDispatcher();

    const toggle = (): void => {
        darkMode = !darkMode;
        document.body.classList.toggle('dark', darkMode);
        localStorage.setItem('darkMode', darkMode ? 'true' : 'false');
        dispatch('toggle', { darkMode });
    };

    onMount(() => {
        const storedDarkMode = localStorage.getItem('darkMode');
        if (storedDarkMode) {
            darkMode = storedDarkMode === 'true';
            document.body.classList.toggle('dark', darkMode);
        }
    });
</script>

<button
    class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
    on:click={toggle}
>
    {#if darkMode}
        Go light
    {:else}
        Go dark
    {/if}
</button>
