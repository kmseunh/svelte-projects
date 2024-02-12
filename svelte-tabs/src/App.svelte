<script lang="ts">
    import { onMount } from 'svelte';
    import axios from 'axios';

    interface User {
        id: number;
        username: string;
        email: string;
        address: {
            street: string;
            suite: string;
            city: string;
            zipcode: string;
            geo: {
                lat: string;
                lng: string;
            };
        };
    }

    let users: User[] = [];
    let activeTab: number = 1;

    const setActiveTab = (tabNumber: number): void => {
        activeTab = tabNumber;
    };

    const fetchData = async () => {
        try {
            const response = await axios.get<User[]>(
                'https://jsonplaceholder.typicode.com/users'
            );
            users = response.data;
        } catch (error) {
            console.log('Error fetching data:', error);
        }
    };

    onMount(fetchData);
</script>

<div class="min-h-screen flex items-center justify-center bg-gray-100">
    <div class="max-w-lg w-full bg-white shadow-md rounded-lg p-6">
        <div class="flex">
            <div class="w-1/3">
                {#each users as user}
                    <div
                        class="p-2 cursor-pointer border-b border-gray-300 hover:bg-gray-300 {activeTab ===
                        user.id
                            ? 'bg-gray-400'
                            : ''}"
                        on:click={() => setActiveTab(user.id)}
                    >
                        {user.username}
                    </div>
                {/each}
            </div>
            <div class="w-2/3 ml-4">
                {#each users as user}
                    <div class={activeTab === user.id ? '' : 'hidden'}>
                        <p class="text-lg font-bold mb-2">{user.username}</p>
                        <p class="mb-2"><strong>Email:</strong> {user.email}</p>
                        <p class="mb-2">
                            <strong>Address:</strong>
                            {user.address.street}, {user.address.suite}, {user
                                .address.city}, {user.address.zipcode}
                        </p>
                    </div>
                {/each}
            </div>
        </div>
    </div>
</div>
