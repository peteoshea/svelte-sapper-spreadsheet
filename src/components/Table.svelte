<script>
  import Row from './Row.svelte';

  let rows = 15;
</script>

{#each Array(rows) as _, row}
  <Row {row} />
{/each}
