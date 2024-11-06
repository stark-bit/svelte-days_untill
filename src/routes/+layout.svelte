<script lang="ts">
	import '../app.css';
	let { children } = $props();
</script>

<div class="dark">
	<div class="text-black dark:text-white">
		{@render children()}
	</div>
</div>

<style>
	:global(:root, body, html) {
		background: #000;
	}
</style>
