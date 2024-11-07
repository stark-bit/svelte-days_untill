<script lang="ts">
	import duration from 'dayjs/plugin/duration';
	import dayjs from 'dayjs';
	let { endDate }: { endDate: string } = $props();

	let countdown = $state();

	$effect(() => {
		dayjs.extend(duration);
		const interval = setInterval(() => {
			const now = dayjs();
			const end = dayjs(endDate);
			const diff = end.diff(now, 'second');
			const duration = dayjs.duration(diff, 'second');

			countdown = `${duration.days()} days, ${duration.hours()} hours, ${duration.minutes()} minutes, ${duration.seconds()} seconds`;
		}, 500);
		return () => clearInterval(interval);
	});
</script>

{#if endDate}
	<div class="text-3xl min-h-[36px] mb-12">
		{countdown}
	</div>
{/if}
