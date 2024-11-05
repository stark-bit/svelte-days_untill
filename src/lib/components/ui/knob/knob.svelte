<script lang="ts">
	import dayjs from 'dayjs';

	let props = $props();
	let interval: number;

	let targetDate = $state(dayjs());

	let now = $state(dayjs());

	$effect(() => {
		targetDate = props.deadline?.replaceAll('-', '.');
		interval = setInterval(() => {
			now = dayjs();
		}, 100);
		return () => clearInterval(interval);
	});
</script>

<div
	class="flex w-[200px] flex-col items-center justify-center rounded-lg border border-white/20 p-5 text-center shadow-sm shadow-black/20 dark:border-white/30 md:p-6 lg:p-6 xl:rounded-xl xl:p-6"
>
	<span class="mb-2 flex items-center justify-center text-base font-black leading-none">
		{dayjs(targetDate).diff(now, props.unit)}
	</span>
	<span class="text-xs font-semibold uppercase leading-none tracking-wide opacity-50 md:text-sm">
		{props.unit}
	</span>
</div>

<style>
</style>
