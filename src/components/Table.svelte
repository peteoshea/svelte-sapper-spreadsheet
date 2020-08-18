<script>
  import Row from './Row.svelte';

  let columns = 8;
  let rows = 15;
</script>

{#each Array(rows) as _, row}
  <Row {row} {columns} />
{/each}
