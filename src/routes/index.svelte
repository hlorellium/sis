<script>
	import Scheme from '../lib/Scheme.svelte';
</script>

<div class="container">
	<Scheme />
</div>

<style>
	.container {
		padding: 25px;
		max-width: 1400px;
		margin: 0 auto;
	}

	@media (max-width: 1350px) {
		.container {
			padding: 8px 16px;
		}
	}
</style>
