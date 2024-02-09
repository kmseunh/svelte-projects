<script lang="ts">
    let rating: number = 0;
    let clicked: boolean = false;

    const setRating = (value: number) => {
        if (!clicked) {
            rating = value;
        }
    };

    const handleClick = (star: number) => {
        clicked = true;
        rating = star;
    };

    const resetRating = (): void => {
        if (!clicked) {
            rating = 0;
        }
    };
</script>

<div class="flex justify-center items-center h-screen">
    {#each Array.from({ length: 5 }, (_, index) => index + 1) as star}
        <span
            class="text-8xl text-gray-400 cursor-pointer transition-colors duration-300 hover:text-yellow-400"
            on:mouseenter={() => setRating(star)}
            on:mouseleave={resetRating}
            on:click={() => handleClick(star)}
        >
            {star <= rating ? '★' : '☆'}
        </span>
    {/each}
</div>
