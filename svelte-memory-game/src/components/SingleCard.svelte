<script lang="ts">
    export let card: { src: string };
    export let imgCover: string;
    export let handleChoice: (card: { src: string }) => void;
    export let flipped: boolean;
    export let disabled: boolean;

    const handleClick = () => {
        if (!disabled) {
            handleChoice(card);
        }
    };
</script>

<div class="card relative">
    <div class:flipped>
        <img
            src={card.src}
            class="front w-[100%] block border-solid border-white border-2"
            alt="card front"
        />
        <img
            src={imgCover}
            class="back rounded-lg border-black border-2"
            on:click={handleClick}
            alt="card back"
        />
    </div>
</div>

<style>
    .card .front {
        transform: rotateY(90deg);
        transition: all ease-in 0.2s;
        position: absolute;
    }
    .flipped .front {
        transform: rotateY(0deg);
        transition-delay: 0.2s;
    }
    .card .back {
        transition: all ease-in 0.2s;
        transition-delay: 0.2s;
    }
    .flipped .back {
        transform: rotateY(90deg);
        transition-delay: 0s;
    }
</style>
