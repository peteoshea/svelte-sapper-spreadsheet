<script>
  import Cell from './Cell.svelte';

  export let columns;
  export let row;
</script>

<style>
  .row {
    display: block;
  }
</style>

<div class="row">
  {#each Array(columns) as _, column}
    <Cell {row} {column} />
  {/each}
</div>
