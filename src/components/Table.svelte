<script>
  import Row from './Row.svelte';

  let columns = 8;
  let data = {};
  let rows = 15;

  const handleChangedCell = (column, row, value) => {
    console.log(column, row, value);
  };
</script>

{#each Array(rows) as _, row}
  <Row {row} {columns} rowData={data[row] || {}} {handleChangedCell} />
{/each}
