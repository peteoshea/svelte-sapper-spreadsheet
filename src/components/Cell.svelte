<script>
  export let row;
  export let column;
  let selected = false;

  const alpha = ' ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('');

  /**
   * Handle clicking a Cell.
   */
  const clicked = () => {
    selected = true;
  };
</script>

<style>
  span.cell {
    width: 80px;
    padding: 4px;
    margin: 0;
    height: 25px;
    box-sizing: border-box;
    position: relative;
    display: inline-block;
    color: black;
    border: 1px solid #cacaca;
    text-align: left;
    vertical-align: top;
    font-size: 14px;
    line-height: 15px;
    overflow: hidden;
    font-family: Calibri, Segoe UI, Thonburi, Arial, Verdana, sans-serif;
  }

  span.cell.first-row,
  span.cell.first-col {
    text-align: center;
    background-color: #f0f0f0;
    font-weight: bold;
  }

  span.cell.selected {
    outline-color: blue;
    outline-style: solid;
  }
</style>

{#if column === 0}
  {#if row === 0}
    <span class="cell first-col first-row" />
  {:else}
    <span class="cell first-col">{row}</span>
  {/if}
{:else}
  {#if row === 0}
    <span class="cell first-row">{alpha[column]}</span>
  {:else}
    <span class="cell {selected ? 'selected' : ''}" on:click={clicked}>
      Cell {alpha[column]}{row}
    </span>
  {/if}
{/if}
