<script lang="ts">
    export let show: boolean;
    export let suggestions: string[] = [];
    export let handleSuggestionClick: (suggestion: string) => void = () => {};

    const handleClick = (suggestion: string): void => {
        handleSuggestionClick(suggestion);
    };
</script>

{#if show && suggestions.length > 0}
    <ul
        class="absolute w-64 mt-2 overflow-y-auto max-h-48 bg-white border border-gray-200 rounded-md shadow-md z-20"
    >
        {#each suggestions as suggestion}
            <li
                class="cursor-pointer py-2 px-4 hover:bg-gray-100"
                on:click={() => handleClick(suggestion)}
            >
                {suggestion}
            </li>
        {/each}
    </ul>
{/if}
