<script>
	import '../app.postcss';
</script>

<div class="center-container w-full">
	<slot />
</div>

<style>
	.center-container {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		min-height: 100vh;
		background: linear-gradient(135deg, #622774 0%, #c53364 50%, #705898 100%);
	}
</style>
