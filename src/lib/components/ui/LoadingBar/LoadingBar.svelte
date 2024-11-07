<script lang="ts">
	import dayjs from 'dayjs';

	let { startDate, endDate } = $props();

	let percentSincePageLoad = $state(0);

	// eslint-disable-next-line @typescript-eslint/no-explicit-any
	const unixDate = (date: any) => {
		return dayjs(date).unix();
	};

	$effect(() => {
		const interval = setInterval(() => {
			percentSincePageLoad =
				1 - (unixDate(endDate) - unixDate(dayjs())) / (unixDate(endDate) - unixDate(startDate));
		}, 500);
		return () => clearInterval(interval);
	});
</script>

{#if startDate}
	<div
		class="md:min-h-13 relative flex min-h-12 w-full items-center gap-[0.5em] rounded-full border-[2px] border-black/30 px-[0.75em] py-[0.5em] text-base dark:border-white md:border-[3px] lg:min-h-12 lg:border-[4px] lg:text-lg xl:min-h-14 xl:text-xl"
	>
		<div
			style={`width: ${parseFloat(percentSincePageLoad * 100 + '').toFixed(4)}%`}
			class="fill absolute bottom-0 left-0 top-0 z-10 flex h-full items-center justify-end rounded-l-full bg-white pr-[0.75em] font-bold dark:bg-white"
		>
			<div class="relative -top-[40px] text-[0.9em] text-black dark:text-white">
				{parseFloat(percentSincePageLoad * 100 + '').toFixed(3)}%
			</div>
		</div>
		<div class="z-20 flex items-center gap-[0.5em] font-bold text-white mix-blend-difference">
			<span class="hidden md:block">Page Load</span>
		</div>
		<i class="fa-sharp fa-solid fa-baby"></i>
		<div
			class="z-20 ml-auto flex items-center gap-[0.5em] font-bold text-white mix-blend-difference"
		>
			<div class="hidden md:block">Deadline</div>
			<span class=""
				><svg
					xmlns="http://www.w3.org/2000/svg"
					viewBox="0 0 512 512"
					width="24"
					height="24"
					fill="currentColor"
					aria-label="Skull Icon"
					class="h-[1.2em] w-[1.2em]"
					><path
						d="M416 398.9c58.5-41.1 96-104.1 96-174.9C512 100.3 397.4 0 256 0S0 100.3 0 224c0 70.7 37.5 133.8 96 174.9L96 512l96 0 0-48 0-16 32 0 0 16 0 48 64 0 0-48 0-16 32 0 0 16 0 48 96 0 0-113.1zM96 256a64 64 0 1 1 128 0A64 64 0 1 1 96 256zm256-64a64 64 0 1 1 0 128 64 64 0 1 1 0-128z"
					></path></svg
				></span
			>
		</div>
	</div>
{/if}

<style>
	.fill {
		width: 0;
		transition: width 0.5s;
	}
</style>
