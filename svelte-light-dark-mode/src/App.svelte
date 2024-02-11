<script lang="ts">
    import Toggle from './components/Toggle.svelte';
    let name: string = 'world';
</script>

<div class="flex flex-col items-center justify-center h-screen">
    <Toggle />

    <h1 class="text-4xl mt-8">Hello {name}!</h1>
</div>

<style>
    :global(body) {
        @apply bg-white text-black;
        transition: background-color 0.3s;
    }

    :global(body.dark) {
        @apply bg-black text-white;
        transition: background-color 0.3s;
    }
</style>
