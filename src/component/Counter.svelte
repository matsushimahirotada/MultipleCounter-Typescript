<script lang="ts">
  export let deleted: boolean;
  export let count: number;

  function counterIncrement(): void {
    //updatemessageを親コンポーネントに送信
    count += 1;
  }

  function counterDecrement(): void {
    //updatemessageを親コンポーネントに送信
    if (count > 0) {
      count -= 1;
    }
  }

  function counterReset(): void {
    //resetmessageを親コンポーネントに送信
    count = 0;
  }

  function deleteCounter(): void {
    deleted = false;
  }
</script>

<!-- svelte-ignore non-top-level-reactive-declaration -->

<button on:click={counterIncrement} class="counterIncrement"> + </button>

<button on:click={counterDecrement} class="counterDecrement"> - </button>

<button on:click={counterReset} class="counterReset"> 0 </button>

<button on:click={deleteCounter} class="deleteCounter"> Delete </button>

<style>
  .counterIncrement {
    background-color: #f00100;
    border: 2px solid #c03c1b;
  }

  .counterIncrement:hover {
    color: #000;
    background: rgb(252, 74, 80);
  }

  .counterDecrement {
    background-color: cyan;
    border: 2px solid #0dcccc;
  }

  .counterDecrement:hover {
    color: #000;
    background: rgb(175, 252, 252);
  }

  .counterReset {
    background-color: #ffff00;
    border: 2px solid #cfcc0a;
  }

  .counterReset:hover {
    color: black;
    background-color: rgb(255, 255, 157);
  }

  .deleteCounter {
    background-color: gray;
    border: 2px solid #807066;
  }

  .deleteCounter:hover {
    color: black;
    background-color: rgb(180, 180, 180);
  }
</style>
