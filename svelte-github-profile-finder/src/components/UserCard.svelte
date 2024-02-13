<script lang="ts">
    export let user;

    const formatDate = (dateString: string): string => {
        const date = new Date(dateString);
        const year = date.getFullYear();
        const month = date.getMonth() + 1;
        const day = date.getDate();

        const formattedMonth = month < 10 ? '0' + month : month;
        const formattedDate = day < 10 ? '0' + day : day;

        return `${year}.${formattedMonth}.${formattedDate}`;
    };
</script>

<div class="bg-white shadow overflow-hidden sm:rounded-lg">
    <div class="px-4 py-5 sm:px-6">
        <h3 class="flex justify-center text-lg font-medium text-gray-900">
            User Information
        </h3>
    </div>
    <img class="mx-auto w-40" src={user.avatar_url} alt="avatar_url" />

    <div class="border-t border-gray-200">
        <dl>
            <div
                class="bg-gray-50 px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6"
            >
                <dt class="text-sm font-medium text-gray-500">Login</dt>
                <dd class="mt-1 text-sm text-gray-900 sm:col-span-2">
                    {user.login}
                </dd>
            </div>
            <div
                class="bg-white px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6"
            >
                <dt class="text-sm font-medium text-gray-500">Name</dt>
                <dd class="mt-1 text-sm text-gray-900 sm:col-span-2">
                    {user.name}
                </dd>
            </div>
            <div
                class="bg-gray-50 px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6"
            >
                <dt class="text-sm font-medium text-gray-500">Location</dt>
                <dd class="mt-1 text-sm text-gray-900 sm:col-span-2">
                    {user.location}
                </dd>
            </div>
            <div
                class="bg-white px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6"
            >
                <dt class="text-sm font-medium text-gray-500">Public Repos</dt>
                <dd class="mt-1 text-sm text-gray-900 sm:col-span-2">
                    {user.public_repos}
                </dd>
            </div>
            <div
                class="bg-gray-50 px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6"
            >
                <dt class="text-sm font-medium text-gray-500">Followers</dt>
                <dd class="mt-1 text-sm text-gray-900 sm:col-span-2">
                    {user.followers}
                </dd>
            </div>
            <div
                class="bg-white px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6"
            >
                <dt class="text-sm font-medium text-gray-500">Following</dt>
                <dd class="mt-1 text-sm text-gray-900 sm:col-span-2">
                    {user.following}
                </dd>
            </div>
            <div
                class="bg-gray-50 px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6"
            >
                <dt class="text-sm font-medium text-gray-500">Created At</dt>
                <dd class="mt-1 text-sm text-gray-900 sm:col-span-2">
                    {formatDate(user.created_at)}
                </dd>
            </div>
        </dl>
    </div>
</div>
