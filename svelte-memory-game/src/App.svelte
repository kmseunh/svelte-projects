<script lang="ts">
    import SingleCard from './components/SingleCard.svelte';

    let imgCover: string =
        'https://img.freepik.com/premium-vector/soccer-ball-logo-illustration-vector_472355-210.jpg';

    const teams: string[] = [
        'https://brandlogos.net/wp-content/uploads/2014/10/real_madrid_cf-brandlogo.net_.png',
        'https://upload.wikimedia.org/wikipedia/en/thumb/c/cc/Chelsea_FC.svg/1200px-Chelsea_FC.svg.png',
        'https://upload.wikimedia.org/wikipedia/commons/thumb/1/1b/FC_Bayern_M%C3%BCnchen_logo_%282017%29.svg/1200px-FC_Bayern_M%C3%BCnchen_logo_%282017%29.svg.png',
        'https://upload.wikimedia.org/wikipedia/en/thumb/7/7a/Manchester_United_FC_crest.svg/1200px-Manchester_United_FC_crest.svg.png',
        'https://upload.wikimedia.org/wikipedia/en/thumb/e/eb/Manchester_City_FC_badge.svg/1200px-Manchester_City_FC_badge.svg.png',
        'https://upload.wikimedia.org/wikipedia/en/thumb/4/47/FC_Barcelona_%28crest%29.svg/1200px-FC_Barcelona_%28crest%29.svg.png',
    ];

    interface Card {
        src: string;
        matched: boolean;
        id: number;
    }

    let cards: Card[] = [];
    let turns: number = 0;
    let choiceOne: Card | null = null;
    let choiceTwo: Card | null = null;
    let disabled: boolean = false;

    const cardImages: Card[] = teams.map((src, index) => ({
        src,
        matched: false,
        id: index,
    }));

    const shuffledCards = (): void => {
        const shuffledCards: Card[] = [...cardImages, ...cardImages]
            .sort(() => Math.random() - 0.5)
            .map((card, index) => ({ ...card, id: index }));
        cards = shuffledCards;
        turns = 0;
    };

    const handleChoice = (card: Card): void => {
        if (disabled) return;
        if (!choiceOne) {
            choiceOne = card;
        } else {
            choiceTwo = card;
            checkMatch();
        }
    };

    const checkMatch = (): void => {
        disabled = true;
        if (choiceOne!.src === choiceTwo!.src) {
            cards = cards.map((card) =>
                card.src === choiceOne!.src ? { ...card, matched: true } : card
            );
        }
        setTimeout(resetTurn, 1000);
    };

    const resetTurn = (): void => {
        choiceOne = null;
        choiceTwo = null;
        turns++;
        disabled = false;
    };

    $: shuffledCards();
</script>

<div
    class="bg-gradient-to-b from-green-500 to-blue-500 text-white min-h-screen text-center p-4"
>
    <div class="max-w-4xl mx-auto">
        <h1 class="text-4xl font-bold mb-8">Soccer Card Mathe</h1>
        <button
            on:click={shuffledCards}
            class="bg-white text-purple-900 py-3 px-6 rounded-full font-bold hover:bg-purple-700 transition duration-300"
            >New Game</button
        >
        <div
            class="card-grid mt-12 grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-8"
        >
            {#each cards as card (card.id)}
                <SingleCard
                    {card}
                    {imgCover}
                    {disabled}
                    {handleChoice}
                    class="w-40 h-56 md:w-48 md:h-64 lg:w-56 lg:h-72 rounded-lg shadow-md transform transition duration-300 ease-in-out hover:scale-105"
                    flipped={card === choiceOne ||
                        card === choiceTwo ||
                        card.matched}
                />
            {/each}
        </div>
        <p class="mt-8 text-xl">Turns: {turns}</p>
    </div>
</div>
