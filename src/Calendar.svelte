<script lang="ts">
  import Week from "./Week.svelte";

  const today = new Date();

  // 今月1日
  const firstDayOfMonth = new Date(today);
  firstDayOfMonth.setDate(1);

  // 1日が属する週の日曜日
  const firstDayOfFirstWeek = new Date(firstDayOfMonth);
  firstDayOfFirstWeek.setDate(1 - firstDayOfMonth.getDay());

  // 表示するすべての日曜日
  const sundays = Array.from(Array(6).keys(), (i) => {
    const sunday = new Date(firstDayOfFirstWeek);
    sunday.setDate(sunday.getDate() + 7 * i);
    return sunday;
  }).filter((date, i) => i === 0 || date.getMonth() === today.getMonth());
</script>

<style>
  h1 {
    margin: 0;
  }

  .calendar {
    display: flex;
    flex-direction: column;
    flex: 1;
    padding-bottom: 18px;
  }

  .week-header {
    display: flex;
  }

  .dow {
    flex: 1;
    border: 1px solid #cccccc;
  }

  .dow:nth-child(n + 2) {
    border-left-width: 0;
  }

  .days {
    display: flex;
    flex-direction: column;
    flex: 1;
  }
</style>

<div>
  <h1>{today.getFullYear()}年{today.getMonth() + 1}月</h1>
</div>
<div class="calendar">
  <div class="week-header">
    {#each ['日', '月', '火', '水', '木', '金', '土'] as dow}
      <div class="dow">{dow}</div>
    {/each}
  </div>
  <div class="days">
    {#each sundays as sunday}
      <Week startDate={sunday} />
    {/each}
  </div>
</div>
