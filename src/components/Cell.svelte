<script>
  import { onMount } from 'svelte';

  export let row;
  export let column;
  let delay = 300;
  let doubleClickOccurred = false;
  let selected = false;
  let timer = 0;

  const alpha = ' ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('');

  /**
   * Used by `componentDid(Un)Mount`, handles the `unselectAll`
   * event response
   */
  const handleUnselectAll = () => {
    if (selected) {
      selected = false;
    }
  };

  // Lifecycle events
  onMount(() => {
    if (typeof window !== 'undefined') {
      window.document.addEventListener('unselectAll', handleUnselectAll);
    }
  });

  /**
   * Handle clicking a Cell.
   */
  const clicked = () => {
    timer = setTimeout(() => {
      if (!doubleClickOccurred) {
        console.log('Click registered');
        emitUnselectAllEvent();
        selected = true;
      }
      doubleClickOccurred = false;
    }, delay);
  };
  const doubleClicked = () => {
    console.log('Double click registered');
    doubleClickOccurred = true;
  };

  /**
   * Emits the `unselectAll` event, used to tell all the other
   * cells to unselect
   */
  const emitUnselectAllEvent = () => {
    const unselectAllEvent = new Event('unselectAll');

    if (typeof window !== 'undefined') {
      window.document.dispatchEvent(unselectAllEvent);
    }
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
    <span
      class="cell {selected ? 'selected' : ''}"
      on:click={clicked}
      on:dblclick={doubleClicked} />
  {/if}
{/if}
