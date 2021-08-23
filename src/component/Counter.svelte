<script lang="ts">
  import { createEventDispatcher } from "svelte";
  const dispatch: any = createEventDispatcher();
  const dispatch2: any = createEventDispatcher();
  export let id: number;
  let count: number;

  function CounterInc(): void {
    //updatemessageを親コンポーネントに送信
    count += 1;
    dispatch2("updatecountorder", { Id: id, Count: count });
  }

  function CounterDec(): void {
    //updatemessageを親コンポーネントに送信
    if (count > 0) {
      count -= 1;
      dispatch2("updatecountorder", { Id: id, Count: count });
    }
  }

  function Counterreset(): void {
    //resetmessageを親コンポーネントに送信
    count = 0;
    dispatch2("updatecountorder", { Id: id, Count: count });
  }

  function deleteCounter(): void {
    //deletemessageを親コンポーネントに送信
    dispatch("deleteorder", { order: id });
  }
</script>

<!-- svelte-ignore non-top-level-reactive-declaration -->

<button on:click={CounterInc} class="CounterInc"> + </button>

<button on:click={CounterDec} class="CounterDec"> - </button>

<button on:click={Counterreset} class="Counterreset"> 0 </button>

<button on:click={deleteCounter} class="deleteCounter"> Delete </button>

<style>
  .CounterInc {
    background-color: #f00100;
    border: 2px solid #c03c1b;
  }

  .CounterInc:hover {
    color: #000;
    background: rgb(252, 74, 80);
  }

  .CounterDec {
    background-color: cyan;
    border: 2px solid #0dcccc;
  }

  .CounterDec:hover {
    color: #000;
    background: rgb(175, 252, 252);
  }

  .Counterreset {
    background-color: #ffff00;
    border: 2px solid #cfcc0a;
  }

  .Counterreset:hover {
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
