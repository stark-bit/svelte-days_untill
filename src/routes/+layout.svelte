<script lang="ts">
	import '../app.css';
	let { children } = $props();
</script>

<div class="dark">
	{@render children()}
</div>

<style>
	:global(:root, body, html) {
		background: #000;
	}
</style>
