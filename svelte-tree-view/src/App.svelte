<script lang="ts">
    import TreeNode from './components/TreeNode.svelte';

    const tree = {
        label: 'USA',
        children: [
            {
                label: 'Florida',
                children: [
                    { label: 'Jacksonville' },
                    {
                        label: 'Orlando',
                        children: [
                            { label: 'Disney World' },
                            { label: 'Universal Studio' },
                            { label: 'Sea World' },
                        ],
                    },
                    { label: 'Miami' },
                ],
            },
            {
                label: 'California',
                children: [
                    { label: 'San Francisco' },
                    { label: 'Los Angeles' },
                    { label: 'Sacramento' },
                ],
            },
        ],
    };
</script>

<TreeNode {tree} />
