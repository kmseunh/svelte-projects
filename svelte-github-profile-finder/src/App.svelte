<script lang="ts">
    import axios from 'axios';
    import UserCard from './components/UserCard.svelte';

    interface User {
        login: string;
        avatar_url: string;
        name: string;
        location: string;
        bio: string;
        public_repos: number;
        followers: number;
        following: number;
        created_at: string;
    }

    let user: User | null = null;
    let userName: string = '';

    const fetchData = async () => {
        try {
            const response = await axios.get<User>(
                `https://api.github.com/users/${userName}`
            );
            user = response.data;
            console.log(user);
        } catch (error) {
            console.log('Error fetching data:', error);
        }
    };
</script>

<div
    class="min-h-screen bg-gray-100 flex items-center justify-center py-8 px-4"
>
    <div class="max-w-md w-full space-y-8">
        <div>
            <h2 class="text-center text-3xl font-extrabold text-gray-900">
                GitHub Profile Finder
            </h2>
        </div>
        <div class="mt-8 space-y-6">
            <div class="rounded-md shadow-sm -space-y-px">
                <div class="mb-4">
                    <input
                        id="username"
                        name="username"
                        type="text"
                        bind:value={userName}
                        class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-t-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
                        placeholder="Enter GitHub username"
                    />
                </div>
                <button
                    on:click={fetchData}
                    type="button"
                    class="w-full flex justify-center py-2 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
                >
                    Search
                </button>
            </div>
        </div>
        {#if user}
            <UserCard {user} />
        {/if}
    </div>
</div>
