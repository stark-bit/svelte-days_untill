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

			const renderTime = (unit?: string) => {
				const years = duration.years();
				const months = duration.months();
				const days = duration.days();
				const hours = duration.hours();
				const minutes = duration.minutes();

				switch (unit) {
					case 'year':
						if (years == 0) return '';
						return years > 1 ? `${years}  ${unit}s,` : `${years} ${unit},`;
					case 'month':
						if (years == 0 && months == 0) return '';
						return months > 1 ? `${months}  ${unit}s,` : `${months} ${unit},`;
					case 'day':
						if (years == 0 && months == 0 && days == 0) return '';
						return days > 1 ? `${days}  ${unit}s,` : `${days} ${unit},`;
					case 'hour':
						if (years == 0 && months == 0 && days <= 0 && hours <= 0) return '';
						return hours > 1 ? `${hours}  ${unit}s,` : `${hours} ${unit},`;
					case 'minute':
						if (years == 0 && months == 0 && days <= 0 && hours <= 0 && minutes == 0) return '';
						return minutes > 1 ? `${minutes}  ${unit}s,` : `${minutes} ${unit},`;
					default:
						return duration.seconds();
				}
			};
			countdown = `${renderTime('year')} ${renderTime('month')} ${renderTime('day')} ${renderTime('hour')} ${renderTime('minute')} ${renderTime()} seconds`;
		}, 500);
		return () => clearInterval(interval);
	});
</script>

{#if endDate}
	<div class="mb-12 min-h-[36px] text-3xl">
		{countdown}
	</div>
{/if}
