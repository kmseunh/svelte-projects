<script lang="ts">
    interface AccodionItem {
        title: string;
        content: string;
    }

    let activeIndex: number = -1;

    const accodionItem: AccodionItem[] = [
        { title: 'Item 1', content: 'Content for Item 1' },
        { title: 'Item 2', content: 'Content for Item 2' },
        { title: 'Item 3', content: 'Content for Item 3' },
    ];

    const handleIndex = (index: number): void => {
        activeIndex = activeIndex === index ? '-1' : index;
    };
</script>

<div class="flex justify-center items-center h-screen bg-gray-900 text-white">
    <div class="flex flex-col">
        {#each accodionItem as item, index}
            <div class="border border-gray-700 rounded m-2 w-52">
                <div
                    class="flex justify-between items-center p-2 bg-gray-800 text-white"
                >
                    <div>{item.title}</div>
                    <button on:click={() => handleIndex(index)}
                        >{activeIndex === index ? '-' : '+'}</button
                    >
                </div>
                {#if activeIndex === index}
                    <div class="bg-gray-900 text-white p-2">
                        <p>{item.content}</p>
                    </div>
                {/if}
            </div>
        {/each}
    </div>
</div>
