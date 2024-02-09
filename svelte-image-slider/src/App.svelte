<script lang="ts">
    import { onMount } from 'svelte';

    let images: string[] = [
        'car1.jpg',
        'car2.jpg',
        'car3.jpg',
        'car4.jpg',
        'car5.jpg',
    ];

    let currentIndex: number = 0;
    let numPages: number = images.length;
    let interval: number | undefined = undefined;
    let autoSlideRunning: boolean = false;

    const nextImage = (): void => {
        currentIndex = (currentIndex + 1) % images.length;
    };

    const prevImage = (): void => {
        currentIndex = (currentIndex - 1 + images.length) % images.length;
    };

    const toggleAutoSlide = (): void => {
        if (autoSlideRunning) {
            clearInterval(interval);
        } else {
            interval = setInterval(nextImage, 5000);
        }
        autoSlideRunning = !autoSlideRunning;
    };

    onMount(() => {
        interval = setInterval(nextImage, 5000);
        autoSlideRunning = true;
    });
</script>

<div class="flex justify-center items-center h-screen relative">
    <div class="relative overflow-hidden">
        <img
            src={`../src/img/${images[currentIndex]}`}
            alt="Slider Image"
            class="image w-600 h-auto transition-opacity duration-500 ease-in-out"
        />

        <button
            on:click={prevImage}
            class="button prev absolute top-1/2 left-4 transform -translate-y-1/2 px-4 py-2 bg-gray-300 text-gray-800 cursor-pointer rounded-full"
        >
            &larr;
        </button>

        <button
            on:click={nextImage}
            class="button next absolute top-1/2 right-4 transform -translate-y-1/2 px-4 py-2 bg-gray-300 text-gray-800 cursor-pointer rounded-full"
        >
            &rarr;
        </button>

        <button
            on:click={toggleAutoSlide}
            class="button auto-slide absolute bottom-4 right-4 px-4 py-2 bg-gray-300 text-gray-800 cursor-pointer rounded-full"
        >
            {#if autoSlideRunning}
                Stop Auto Slide
            {:else}
                Start Auto Slide
            {/if}
        </button>
    </div>

    <div class="absolute bottom-56 flex justify-center w-full">
        {#each Array(numPages) as _, i}
            <span
                class:active={i === currentIndex}
                class="dot inline-block w-4 h-4 rounded-full bg-gray-400 mx-2 cursor-pointer"
            ></span>
        {/each}
    </div>
</div>

<style>
    .dot.active {
        background-color: #333;
    }

    .image {
        max-width: 100%; /* 이미지 최대 너비 조정 */
        height: auto; /* 높이 자동 조정 */
    }

    .button {
        z-index: 1; /* 이미지 위로 */
    }
</style>
