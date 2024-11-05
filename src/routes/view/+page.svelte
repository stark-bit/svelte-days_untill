<script lang="ts">
	import Knob from '$lib/components/ui/knob/knob.svelte';
	import LoadingBar from '$lib/components/ui/LoadingBar/LoadingBar.svelte';

	let deadline = $state();

	$effect(() => {
		const searchParams = new URLSearchParams(window.location.search);
		deadline = searchParams.get('deadline');
	});
</script>

<main class="container m-auto">
	<section
		class="grid min-h-svh grid-cols-1 items-center justify-center justify-items-center"
	>
		<h1
			class="mb-12 text-3xl font-extrabold leading-snug text-white md:text-4xl lg:text-5xl xl:text-5xl 2xl:text-5xl"
		>
			Choose your deadline
		</h1>
		<LoadingBar {deadline} />
		<div
			class="mt-12 grid grid-cols-1 justify-items-center gap-3 text-white sm:grid-cols-3 md:grid-cols-3 lg:grid-cols-4 lg:gap-4 xl:grid-cols-5 xl:gap-5 2xl:grid-cols-7"
		>
			<Knob unit="years" {deadline} />
			<Knob unit="months" {deadline} />
			<Knob unit="weeks" {deadline} />
			<Knob unit="days" {deadline} />
			<Knob unit="hours" {deadline} />
			<Knob unit="minutes" {deadline} />
			<Knob unit="seconds" {deadline} />
		</div>
	</section>
</main>
