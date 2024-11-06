<script lang="ts">
	import DayGrid from '$lib/components/ui/DayGrid/DayGrid.svelte';
	import Knob from '$lib/components/ui/knob/knob.svelte';
	import LoadingBar from '$lib/components/ui/LoadingBar/LoadingBar.svelte';

	let startDate: string = $state('');
	let endDate: string = $state('');

	$effect(() => {
		const searchParams = new URLSearchParams(window.location.search);
		startDate = searchParams.get('startDate') ?? '';
		endDate = searchParams.get('endDate') ?? '';
	});
</script>

<main class="container m-auto">
	<section class="grid min-h-svh grid-cols-1 items-center justify-center justify-items-center">
		<h1
			class="mb-12 text-3xl font-extrabold leading-snug text-white md:text-4xl lg:text-5xl xl:text-5xl 2xl:text-5xl"
		>
			Choose your end Date
		</h1>
		<LoadingBar {endDate} />
		<div
			class="mt-12 grid grid-cols-1 justify-items-center gap-3 text-white sm:grid-cols-3 md:grid-cols-3 lg:grid-cols-4 lg:gap-4 xl:grid-cols-5 xl:gap-5 2xl:grid-cols-7"
		>
			<Knob unit="years" {endDate} />
			<Knob unit="months" {endDate} />
			<Knob unit="weeks" {endDate} />
			<Knob unit="days" {endDate} />
			<Knob unit="hours" {endDate} />
			<Knob unit="minutes" {endDate} />
			<Knob unit="seconds" {endDate} />
		</div>
	</section>

	<section class="flex flex-col pb-32">
		<h2 class="text-bold mb-12 mt-12 text-3xl">Days</h2>
		<DayGrid {startDate} {endDate} unit={'days'} />
	</section>
</main>
