<script lang="ts">
    import Result from './Result.svelte';

    let text: string = '';
    let started: boolean = false;
    let startTime: Date | undefined;
    let elapsedTime: number | undefined;
    let wordCount: number = 0;
    let typingSpeed: number = 0;

    const startTest = (): void => {
        started = true;
        startTime = new Date();
        setTimeout(() => {
            document.getElementById('typingTextArea')?.focus();
        }, 0);
    };

    const endTest = (): void => {
        if (startTime && text.trim() !== '') {
            elapsedTime = (Date.now() - startTime.getTime()) / 1000;
            wordCount = text.trim().split(/\s+/).length;
            typingSpeed = Math.round(wordCount / (elapsedTime / 60));
            started = false;
        }
    };

    const handleKeyDown = (event: KeyboardEvent): void => {
        if (event.key === 'Enter') {
            endTest();
        }
    };
</script>

<div
    class="min-h-screen flex items-center justify-center bg-gray-900 text-white"
>
    <div class="w-96 p-4 bg-gray-800 rounded-lg shadow-lg">
        <h1 class="text-3xl font-bold text-center mb-4">Typing Speed Test</h1>
        {#if !started}
            <textarea
                id="typingTextArea"
                class="w-full h-48 p-2 border rounded bg-gray-700 text-white mb-4"
                bind:value={text}
            ></textarea>
            <div class="text-center">
                <button
                    class="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600"
                    on:click={startTest}>Start Test</button
                >
            </div>
        {:else}
            <textarea
                id="typingTextArea"
                class="w-full h-48 p-2 border rounded bg-gray-700 text-white mb-4"
                bind:value={text}
                on:keydown={handleKeyDown}
            ></textarea>
            <div class="text-center">
                <button
                    class="px-4 py-2 bg-red-500 text-white rounded hover:bg-red-600"
                    on:click={endTest}>End Test</button
                >
            </div>
        {/if}

        {#if typingSpeed > 0}
            <Result {typingSpeed} />
        {/if}
    </div>
</div>
