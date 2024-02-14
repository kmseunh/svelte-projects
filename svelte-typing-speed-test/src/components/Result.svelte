<script lang="ts">
    export let typingSpeed: number;
</script>

{#if typingSpeed > 0}
    <p class="mt-4 text-center text-gray-300">
        Your typing speed: {typingSpeed} words per minute
    </p>
{/if}
