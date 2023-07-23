<script lang="ts">
	import { onMount } from 'svelte';
	import { Button, Card } from 'flowbite-svelte';

	const url = 'https://api.recursionist.io/random-user';
	let show = false;

	interface UserProfile {
		firstName: string;
		lastName: string;
		website: string;
		birthday: string;
		occupation: string;
		bio: string;
		skills: string[];
	}

	let userProfile: UserProfile = {
		firstName: '',
		lastName: '',
		website: '',
		birthday: '',
		occupation: '',
		bio: '',
		skills: []
	};

	onMount(async () => {
		const res = await fetch(url);
		userProfile = await res.json();
		console.log(userProfile);
	});
</script>

{#if !show}
	<Button
		on:click={() => {
			show = true;
		}}
		color="light"
		variant="contained">Show Profile Card!</Button
	>
{:else}
	<Card class="mt-5 w-full max-w-md mx-auto bg-white rounded-xl shadow-md overflow-hidden">
		<div class="p-8">
			<h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900">
				{userProfile.firstName}
				{userProfile.lastName}
			</h5>
			<p class="mb-3 text-gray-700">
				{userProfile.website}
			</p>
			<p class="mb-3 text-gray-700">
				{userProfile.birthday}
			</p>
			<p class="mb-3 text-gray-700">
				{userProfile.occupation}
			</p>
			<p class="font-normal text-gray-700 leading-tight">
				{userProfile.bio}
			</p>
			<div class="flex flex-wrap mt-6 -mx-1">
				{#each userProfile.skills as skill}
					<span
						class="px-2 py-1 mb-1 mr-1 text-sm font-semibold text-gray-700 bg-gray-200 rounded-full"
					>
						{skill}
					</span>
				{/each}
			</div>
		</div>
	</Card>
{/if}
