<script>
  import Cell from './Cell.svelte';

  export let columns;
  export let handleChangedCell;
  export let row;
  export let rowData;
</script>

<style>
  .row {
    display: block;
  }
</style>

<div class="row">
  {#each Array(columns) as _, column}
    <Cell {row} {column} value={rowData[column] || ''} onChangedValue={handleChangedCell} />
  {/each}
</div>
