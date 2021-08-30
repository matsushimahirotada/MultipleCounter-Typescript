<script lang="ts">
  export let deleted: boolean;
  export let count: number;

  function counterIncrement(): void {
    count += 1;
  }

  function counterDecrement(): void {
    if (count > 0) {
      count -= 1;
    }
  }

  function counterReset(): void {
    count = 0;
  }

  function deleteCounter(): void {
    deleted = true;
  }
</script>

<button on:click={counterIncrement} class="counterIncrement"> + </button>

<button on:click={counterDecrement} class="counterDecrement"> - </button>

<button on:click={counterReset} class="counterReset"> 0 </button>

<button on:click={deleteCounter} class="deleteCounter"> Delete </button>

<style>
  .counterIncrement {
    background-color: #f00100;
    border: 2px solid #c03c1b;
    cursor: pointer;
  }

  .counterIncrement:hover {
    color: #000;
    background: rgb(252, 74, 80);
  }

  .counterDecrement {
    background-color: cyan;
    border: 2px solid #0dcccc;
    cursor: pointer;
  }

  .counterDecrement:hover {
    color: #000;
    background: rgb(175, 252, 252);
  }

  .counterReset {
    background-color: #ffff00;
    border: 2px solid #cfcc0a;
    cursor: pointer;
  }

  .counterReset:hover {
    color: black;
    background-color: rgb(255, 255, 157);
  }

  .deleteCounter {
    background-color: gray;
    border: 2px solid #807066;
    cursor: pointer;
  }

  .deleteCounter:hover {
    color: black;
    background-color: rgb(180, 180, 180);
  }
</style>
