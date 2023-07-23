<script>
	import { Alert, GradientButton } from 'flowbite-svelte';
</script>

<div class="p-8">
	<Alert>
		<span class="font-medium">Info alert!</span> Change a few things up and try submitting again.
	</Alert>
</div>

<GradientButton href="/profile" class="m-10 h-16" variant="contained">User Profile Card</GradientButton>
<GradientButton href="/library" class="m-10 h-16" variant="contained">Library Application</GradientButton>