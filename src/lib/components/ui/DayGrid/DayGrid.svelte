<script lang="ts">
	import cn from 'clsx';
	import dayjs from 'dayjs';
	type Unit = 'days' | 'hours' | 'minutes' | 'months' | 'years';
	let { startDate, endDate }: { startDate: string; endDate: string; unit: Unit } = $props();

	type Day = { date: string; past: boolean; today: boolean; dNum: number };

	const createDayArr = (start: string, end: string): Day[] => {
		const totalDays = dayjs(end).diff(start, 'days');
		const dayArr = Array(totalDays).fill('');
		const firstDayNumber = dayjs(startDate).day();

		return dayArr.map((_: unknown, index: number) => {
			let day = { date: '', past: false, today: false, dNum: 0 };
			day.dNum = (index + firstDayNumber) % 7;
			// @ts-expect-error - don't care
			day.date = dayjs(startDate).add(index + 1, 'day');
			day.past = dayjs().diff(dayjs(day.date), 'days') < 0;
			let hourDiff = Math.floor(dayjs().diff(dayjs(day.date), 'days', true));
			day.today = hourDiff + 1 == 0;

			return day;
		});
	};
	const createWeekArr = (days: Day[]): [Day][] => {
		// split days into weeks, each week starts with monday
		const weeks = [];
		// @ts-expect-error - don't care
		let week = [];
		days.forEach((day, i) => {
			if (day.dNum === 1 && i !== 0) {
				// @ts-expect-error - don't care
				weeks.push(week);
				week = [];
			}
			week.push(day);
		});
		// @ts-expect-error - don't care
		weeks.push(week);
		// @ts-expect-error - don't care
		return weeks;
	};
</script>

<div class="week flex flex-wrap gap-2 gap-y-10">
	{#if startDate}
		{#each createWeekArr(createDayArr(startDate, endDate)) as weeks}
			<div class="week flex flex-col gap-2">
				{#each weeks as day}
					<div
						title={day.date}
						class={cn(
							'day life-square relative mr-2 h-full w-full rounded-full bg-black',
							!day.past ? 'dark:bg-white/40' : 'dark:bg-white/70',
							day.today && 'scale-150 bg-[green!important]'
						)}
					></div>
				{/each}
			</div>
		{/each}
	{/if}
</div>

<style>
	.day {
		width: 10px;
		height: 10px;
	}
</style>
