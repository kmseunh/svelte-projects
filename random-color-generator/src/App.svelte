<script lang="ts">
    const HEX_VALUES: string = '0123456789ABCDEF';
    const RGB_VALUES: number = 255;

    const createHexColor = (): string => {
        let hexColor: string = '#';
        for (let i = 0; i < 6; i++) {
            hexColor +=
                HEX_VALUES[Math.floor(Math.random() * HEX_VALUES.length)];
        }
        return hexColor;
    };

    const createRGBColor = (): string => {
        const r = Math.floor(Math.random() * (RGB_VALUES + 1));
        const g = Math.floor(Math.random() * (RGB_VALUES + 1));
        const b = Math.floor(Math.random() * (RGB_VALUES + 1));
        let rgb = `RGB(${r}, ${g}, ${b})`;
        return rgb;
    };

    const generateRandomColor = (): string => {
        return Math.random() < 0.5 ? createHexColor() : createRGBColor();
    };

    const setColor = (color: string) => {
        document.body.style.backgroundColor = color;
        const colorElement = document.getElementById('color');
        if (colorElement) {
            colorElement.innerText = color;
        }
    };
</script>

<div class="flex justify-center mt-3 gap-4">
    <div>
        <button class="button-style" on:click={() => setColor(createHexColor())}
            >Create HEX Color</button
        >
        <button class="button-style" on:click={() => setColor(createRGBColor())}
            >Create RGB Color</button
        >
        <button
            class="button-style"
            on:click={() => setColor(generateRandomColor())}
            >Generate Random Color</button
        >
    </div>
    <div id="color" class="color-display"></div>
</div>

<style>
    .button-style {
        @apply bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow;
    }

    .color-display {
        @apply absolute p-4 bottom-10 font-bold text-9xl text-white;
    }
</style>
