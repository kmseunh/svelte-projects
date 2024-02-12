<script lang="ts">
    import { createEventDispatcher } from 'svelte';

    export let title: string = 'Default Title';
    export let content: string = 'Default Content';
    export let isOpen: boolean = false;

    const dispatch = createEventDispatcher();

    const closeModal = (): void => {
        isOpen = false;
        dispatch('close');
    };
</script>

{#if isOpen}
    <dialog open on:close={closeModal}>
        <div class="modal-content">
            <button class="close-button" on:click={closeModal}>X</button>
            <h1 class="text-4xl mb-4">{title}</h1>
            <p class="text-lg">{content}</p>
        </div>
    </dialog>
{/if}

<style>
    dialog {
        position: fixed;
        top: 0;
        left: 0;
        width: 100vw;
        height: 100vh;
        background-color: rgba(0, 0, 0, 0.5);
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .modal-content {
        background-color: white;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
        position: relative;
        width: 80%;
        max-width: 500px;
    }

    .close-button {
        position: absolute;
        top: 10px;
        right: 10px;
        background: none;
        border: none;
        font-size: 1.2rem;
        cursor: pointer;
        padding: 0;
    }
</style>
