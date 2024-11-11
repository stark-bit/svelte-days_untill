<script lang="ts">
	import dayjs from 'dayjs';
	let {unit, endDate } = $props();

	let now = $state(dayjs());
	let value = $derived(dayjs(endDate).diff(now, unit));


	$effect(() => {
		const interval = setInterval(() => {
			now = dayjs();
		}, 100);
		return () => clearInterval(interval);
	});
</script>

{#if value && unit}
	<div
		class="flex w-[150px] flex-col items-center justify-center rounded-lg border border-white/20 p-5 text-center shadow-sm shadow-black/20 dark:border-white/30 md:p-6 lg:p-6 xl:rounded-xl xl:p-6"
	>
		<span class="mb-2 flex items-center justify-center text-base font-black leading-none">
			{new Intl.NumberFormat('en-GB' ).format(  value)}
		</span>
		<span class="text-xs font-semibold uppercase leading-none tracking-wide opacity-50 md:text-sm">
			{unit}
		</span>
	</div>
{/if}

