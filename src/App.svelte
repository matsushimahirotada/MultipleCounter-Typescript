<script lang="ts">
  import Counter from "./component/Counter.svelte";
  import Box from "./component/Box.svelte";
  import { fly } from "svelte/transition";

  interface counterObj {
    id: number;
    name: string;
    count: number;
  }

  let currentId: number = 0;
  $: nextId = currentId + 1;

  let counterArray: counterObj[] = [{ id: 0, name: "new", count: 0 }];

  let sum: number = 0; //各カウンターのカウント合計値

  function addCounter(): void {
    //カウンターを増やす関数
    counterArray = [].concat(counterArray, {
      id: nextId,
      name: "new",
      count: 0,
    });
    currentId += 1;
  }

  function deleteCounter(event): void {
    //カウンターを減らす関数
    const id: number = event.detail.id; //deleteされたカウンターのidを取得
    const index: number = counterArray.findIndex(
      (element: counterObj) => element.id === id
    );
    if (index !== -1) {
      const firstArray: counterObj[] = counterArray.slice(0, index);
      const secondArray: counterObj[] = counterArray.slice(index + 1);
      counterArray = [].concat(firstArray, secondArray);
      sum = counterArray.reduce(
        (sum: number, element) => sum + element.count,
        0
      );
    }
  }

  function updateCount(event): void {
    const id: number = event.detail.id; //カウント値が変動したカウンターのidを取得
    const count: number = event.detail.count; //最新のカウント値
    const index: number = counterArray.findIndex(
      (element: counterObj) => element.id === id
    );
    if (index !== -1) {
      counterArray[index] = {
        id: id,
        name: counterArray[index].name,
        count: count,
      };
      sum = counterArray.reduce(
        (sum: number, element) => sum + element.count,
        0
      ); //各カウンターのカウント合計値更新
    }
  }
</script>

<!-- svelte-ignore non-top-level-reactive-declaration -->

<h1>サンプル：カウンター作成サイト</h1>

<p>
  <button on:click={addCounter} class="newCounter"
    >新しいカウンターを作成</button
  >
</p>

{#each counterArray as counter (counter.id)}
  <Box>
    <input bind:value={counter.name} />

    {#key counter.count}
      <span
        class="counterCount"
        style="display: inline-block"
        in:fly={{ y: -20 }}>{counter.count}</span
      >
    {/key}

    <Counter
      on:deleteCounterOrder={deleteCounter}
      on:updateCountOrder={updateCount}
      id={counter.id}
    />
  </Box>
{/each}

<div>
  title list:
  {#each counterArray as { id, name }}
    {#if id === currentId}
      {name}
    {:else}
      {name},
    {/if}
  {/each}
</div>

<div>
  {#key sum}
    sum of count:<span
      class="counterCount"
      style="display: inline-block"
      in:fly={{ y: -20 }}>{sum}</span
    >
  {/key}
</div>

<style>
  .newCounter {
    color: #fff;
    background-color: #eb6100;
  }

  .newCounter:hover {
    color: #fff;
    background: #f56500;
  }

  .counterCount {
    margin: 20px;
  }
</style>
