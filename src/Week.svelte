<script lang="ts">
  import Day from "./Day.svelte";

  export let startDate: Date;

  // 1週間のDateオブジェクト
  const week = Array.from(Array(7).keys(), (i) => {
    const date = new Date(startDate);
    date.setDate(startDate.getDate() + i);
    return date;
  });
</script>

<style>
  div {
    display: flex;
    flex: 1;
  }
</style>

<div class="week">
  {#each week as date}
    <Day {date} />
  {/each}
</div>
