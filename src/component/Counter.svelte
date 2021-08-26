<script lang="ts">
  import { createEventDispatcher } from "svelte";
  export let valid: boolean;
  export let count: number;
  const dispatch = createEventDispatcher<{
    deleteCounterOrder: { id: string; count: number };
  }>();

  function counterInc(): void {
    //updatemessageを親コンポーネントに送信
    count += 1;
  }

  function counterDec(): void {
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
    //deletemessageを親コンポーネントに送信
  }
</script>

<!-- svelte-ignore non-top-level-reactive-declaration -->

<button on:click={counterInc} class="counterInc"> + </button>

<button on:click={counterDec} class="counterDec"> - </button>

<button on:click={counterReset} class="counterReset"> 0 </button>

<button on:click={deleteCounter} class="deleteCounter"> Delete </button>

<style>
  .counterInc {
    background-color: #f00100;
    border: 2px solid #c03c1b;
  }

  .counterInc:hover {
    color: #000;
    background: rgb(252, 74, 80);
  }

  .counterDec {
    background-color: cyan;
    border: 2px solid #0dcccc;
  }

  .counterDec:hover {
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
