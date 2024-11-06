<script lang="ts">
	import Countdown from '$lib/components/ui/Countdown/Countdown.svelte';
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
    <Countdown {endDate} />
		<LoadingBar {startDate} {endDate} />
		<div
			class="mt-12 grid grid-cols-1 sm:grid-cols-2 justify-items-center gap-3 text-white  md:grid-cols-3 lg:grid-cols-4 lg:gap-4 xl:grid-cols-5 xl:gap-5 xl3:gap-10 2xl:grid-cols-6"
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
