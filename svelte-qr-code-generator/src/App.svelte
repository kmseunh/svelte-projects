<script lang="ts">
    import { onMount } from 'svelte';
    import QRCode from 'svelte-qrcode';
    import { createEventDispatcher } from 'svelte';

    export let text: string = '';

    const dispatch = createEventDispatcher();

    let inputValue: string = '';
    let isButtonClicked: boolean = false;

    onMount(() => {
        inputValue = text;
    });

    const generateQRCode = (): void => {
        dispatch('generate', {
            value: inputValue,
        });
        isButtonClicked = true;
    };

    $: {
        text = inputValue;
    }
</script>

<div class="flex flex-col justify-center items-center h-screen">
    <h1 class="text-3xl font-bold mb-4">QR Code Generator</h1>
    <input
        type="text"
        class="border border-gray-300 rounded-md px-4 py-2 mb-4"
        bind:value={inputValue}
        placeholder="Enter text for QRCode"
    />
    <button
        class="bg-blue-500 hover:bg-blue-600 text-white font-bold py-2 px-4 rounded"
        on:click={generateQRCode}>Generate QR Code</button
    >
    {#if text && isButtonClicked}
        <div class="mt-4">
            <QRCode value={text} />
        </div>
    {/if}
</div>
