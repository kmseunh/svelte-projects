<script lang="ts">
    import Modal from './components/Modal.svelte';

    let showModal: boolean = false;
    let modalTitle: string = 'Special Title';
    let modalContent: string = 'Special Content';

    const toggleModal = (): void => {
        showModal = !showModal;
    };
</script>

<div class="flex justify-center items-center h-screen">
    <button
        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
        on:click={toggleModal}>Toggle Modal</button
    >
</div>

<Modal bind:isOpen={showModal} title={modalTitle} content={modalContent} />
