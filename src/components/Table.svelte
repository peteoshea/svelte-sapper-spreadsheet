<script>
  import Row from './Row.svelte';
  import { onMount } from 'svelte';

  export let tableIdentifier;

  let columns = 8;
  let data = {};
  let rows = 15;

  onMount(() => {
    if (typeof window !== 'undefined') {
      const localStorageData = window.localStorage.getItem(tableIdentifier);
      if (localStorageData) {
        data = JSON.parse(localStorageData);
      }
    }
  });

  const handleChangedCell = (column, row, value) => {
    if (!data[row]) {
      data[row] = {};
    }
    data[row][column] = value;

    if (window && window.localStorage) {
      window.localStorage.setItem(tableIdentifier, JSON.stringify(data));
    }
  };
</script>

{#each Array(rows) as _, row}
  <Row {row} {columns} rowData={data[row] || {}} {handleChangedCell} />
{/each}
