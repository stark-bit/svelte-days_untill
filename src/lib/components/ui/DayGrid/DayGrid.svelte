<script lang='ts'>
let { startDate, endDate } = $props();

console.log('rei date',startDate);

</script>

<div class="week flex flex-col gap-2">
  <div
class="day life-square bg-black dark:bg-white/70 relative h-full w-full rounded-full"
></div>
  <div
class="day life-square bg-black dark:bg-white/70 relative h-full w-full rounded-full"
></div>
  <div
class="day life-square bg-black dark:bg-white/70 relative h-full w-full rounded-full"
></div>
  <div
class="day life-square bg-black dark:bg-white/70 relative h-full w-full rounded-full"
></div>
  <div
class="day life-square bg-black dark:bg-white/70 relative h-full w-full rounded-full"
></div>
  <div
class="day life-square bg-black dark:bg-white/70 relative h-full w-full rounded-full"
></div>
  <div
class="day life-square bg-black dark:bg-white/70 relative h-full w-full rounded-full"
></div>
  </div>


<style>
.week {
}
.day {
    width: 10px;
    height: 10px;
}
</style>

