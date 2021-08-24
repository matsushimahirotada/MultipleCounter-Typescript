<script lang="ts">
  import Counter from "./component/Counter.svelte";
  import Box from "./component/Box.svelte";
  import { fly } from "svelte/transition";

  interface counterObj {
    id: number;
    name: string;
    count: number;
  }

  let currentid: number = 0;
  $: nextid = currentid + 1;

  let counterArray: counterObj[] = [{ id: 0, name: "new", count: 0 }];

  let sum: number = 0; //各カウンターのカウント合計値

  function addCounter(): void {
    //カウンターを増やす関数
    const result = [].concat(counterArray, {
      id: nextid,
      name: "new",
      count: 0,
    });
    counterArray = result;
    currentid += 1;
  }

  const dedupeArray = (ary, key) => {
    let values = [];
    return ary.filter((e) => {
      if (values.indexOf(e[key]) === -1) {
        values = [].concat(values, e[key]);
        return e;
      }
    });
  };

  function deleteCounter(event): void {
    //カウンターを減らす関数
    const id: number = event.detail.order; //deleteされたカウンターのidを取得
    const index: number = counterArray.findIndex(
      (element: counterObj) => element.id === id
    );
    if (index !== -1) {
      const firstArray: counterObj[] = counterArray.slice(0, index);
      const secondArray: counterObj[] = counterArray.slice(index + 1);
      const tmpArray = [].concat(firstArray, secondArray);
      counterArray = tmpArray; //dedupeArray(tmpArray, "id");
      sum = counterArray.reduce(
        (sum: number, element) => sum + element.count,
        0
      );
    }
  }

  function updateCount(event): void {
    const id: number = event.detail.Id; //カウント値が変動したカウンターのidを取得
    const count: number = event.detail.Count; //最新のカウント値
    const index: number = counterArray.findIndex(
      (element: counterObj) => element.id === id
    );
    counterArray[index] = {
      id: id,
      name: counterArray[index].name,
      count: count,
    };
    sum = counterArray.reduce((sum: number, element) => sum + element.count, 0); //各カウンターのカウント合計値更新
  }
</script>

<!-- svelte-ignore non-top-level-reactive-declaration -->

<h1>サンプル：カウンター作成サイト</h1>

<p>
  <button on:click={addCounter} class="newcounter"
    >新しいカウンターを作成</button
  >
</p>

{#each counterArray as counter (counter.id)}
  <Box>
    <input bind:value={counter.name} />

    {#key counter.count}
      <span
        class="Countercount"
        style="display: inline-block"
        in:fly={{ y: -20 }}>{counter.count}</span
      >
    {/key}

    <Counter
      on:deleteorder={deleteCounter}
      on:updatecountorder={updateCount}
      id={counter.id}
    />
  </Box>
{/each}

<div>
  title list:
  {#each counterArray as { id, name }}
    {#if id === currentid}
      {name}
    {:else}
      {name},
    {/if}
  {/each}
</div>

<div>
  {#key sum}
    sum of count:<span
      class="Countercount"
      style="display: inline-block"
      in:fly={{ y: -20 }}>{sum}</span
    >
  {/key}
</div>

<style>
  .newcounter {
    color: #fff;
    background-color: #eb6100;
  }

  .newcounter:hover {
    color: #fff;
    background: #f56500;
  }

  .Countercount {
    margin: 20px;
  }
</style>
