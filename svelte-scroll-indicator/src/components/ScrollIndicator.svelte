<script>
    import { onDestroy, onMount } from 'svelte';

    let scrollPercentage = 0;

    const calculateScrollPercentage = () => {
        const scrollableHeight =
            document.documentElement.scrollHeight - window.innerHeight;
        scrollPercentage = (window.scrollY / scrollableHeight) * 100;
    };

    const handleScroll = () => {
        requestAnimationFrame(calculateScrollPercentage);
    };

    onMount(() => {
        calculateScrollPercentage();
        window.addEventListener('scroll', handleScroll);

        return () => {
            window.removeEventListener('scroll', handleScroll);
        };
    });

    onDestroy(() => {
        window.removeEventListener('scroll', handleScroll);
    });
</script>

<div class="scroll-indicator h-8 bg-black fixed top-0 left-0 w-full z-50">
    <div
        class="scroll-indicator-progress h-full bg-yellow-400"
        style="width: {scrollPercentage}%"
    ></div>
</div>
