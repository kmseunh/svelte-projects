<script lang="ts">
    let password: string = '';
    let length: number = 12;
    let includeUppercase: boolean = true;
    let includeLowercase: boolean = true;
    let includeNumbers: boolean = true;
    let includeSymbols: boolean = true;
    let showPassword: boolean = false;

    const generatePassword = (): void => {
        const uppercaseChars: string = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
        const lowercaseChars: string = 'abcdefghijklmnopqrstuvwxyz';
        const numberChars: string = '0123456789';
        const symbolChars: string = '!@#$%^&*()_+{}[]';

        let charset: string = '';

        if (includeUppercase) charset += uppercaseChars;
        if (includeLowercase) charset += lowercaseChars;
        if (includeNumbers) charset += numberChars;
        if (includeSymbols) charset += symbolChars;

        let newPassword: string = '';
        for (let i = 0; i < length; i++) {
            const randomIndex = Math.floor(Math.random() * charset.length);
            newPassword += charset[randomIndex];
        }
        password = newPassword;
    };
</script>

<main
    class="font-sans flex flex-col items-center justify-center min-h-screen bg-gray-900 text-white"
>
    <div class="bg-gray-800 p-6 rounded-lg shadow-lg">
        <h1 class="text-3xl font-bold mb-4">Password Generator</h1>
        <label class="flex items-center mb-2">
            <span class="mr-2">Length:</span>
            <input
                type="number"
                class="w-16 p-2 border border-gray-300 text-black"
                bind:value={length}
                min="4"
                max="32"
            />
        </label>
        <label class="flex items-center mb-2">
            <input
                type="checkbox"
                class="mr-2"
                bind:checked={includeUppercase}
            />
            Uppercase
        </label>
        <label class="flex items-center mb-2">
            <input
                type="checkbox"
                class="mr-2"
                bind:checked={includeLowercase}
            />
            Lowercase
        </label>
        <label class="flex items-center mb-2">
            <input type="checkbox" class="mr-2" bind:checked={includeNumbers} />
            Numbers
        </label>
        <label class="flex items-center mb-2">
            <input type="checkbox" class="mr-2" bind:checked={includeSymbols} />
            Symbols
        </label>
        <button
            class="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600 focus:outline-none focus:bg-blue-600"
            on:click={generatePassword}>Generate Password</button
        >
        {#if password}
            <div class="mt-4">
                <h2 class="text-xl font-bold mb-2">Generated Password:</h2>
                <input
                    type="checkbox"
                    class="mr-2"
                    bind:checked={showPassword}
                    id="togglePassword"
                />
                <label for="togglePassword">Show Password</label>
                {#if showPassword}
                    <input
                        type="text"
                        class="w-full p-2 border border-gray-300 rounded text-black"
                        bind:value={password}
                        readonly
                    />
                {:else}
                    <input
                        type="password"
                        class="w-full p-2 border border-gray-300 rounded text-black"
                        bind:value={password}
                        readonly
                    />
                {/if}
            </div>
        {/if}
    </div>
</main>
