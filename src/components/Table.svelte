<script>
  let rows = 15;
</script>

{#each Array(rows) as _, row}
  Row {row}
  <br />
{/each}
