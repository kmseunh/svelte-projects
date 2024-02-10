<script lang="ts">
    import { onMount } from 'svelte';

    interface TreeNode {
        label: string;
        children?: TreeNode[];
    }

    export let tree: TreeNode;

    let expansionState: { [label: string]: boolean } = {};

    const toggleExpansion = (label: string): void => {
        expansionState[label] = !expansionState[label];
        expansionState = { ...expansionState };
    };

    const initializeExpansionState = (node: TreeNode): void => {
        if (node.children) {
            expansionState[node.label] = false;
            node.children.forEach(initializeExpansionState);
        }
    };

    onMount(() => {
        initializeExpansionState(tree);
    });

    let arrowDown: boolean;
    $: arrowDown = expansionState[tree.label];
</script>

<ul class="ml-2 space-y-1">
    {#if tree.children}
        <li>
            <span
                class="flex items-center cursor-pointer"
                on:click={() => toggleExpansion(tree.label)}
            >
                <span class:arrowDown class="mr-2">{arrowDown ? '-' : '+'}</span
                >
                {tree.label}
            </span>
            {#if arrowDown}
                <ul class="pl-4">
                    {#each tree.children as child}
                        <li>
                            <svelte:self tree={child} />
                        </li>
                    {/each}
                </ul>
            {/if}
        </li>
    {:else}
        <li>{tree.label}</li>
    {/if}
</ul>
