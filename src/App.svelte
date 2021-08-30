<script lang="ts">
  import Counter from "./component/Counter.svelte";
  import Box from "./component/Box.svelte";
  import { fly } from "svelte/transition";

  interface ICounter {
    /** deleteされているかを判断するflag変数 */
    deleted: boolean;
    name: string; // カウンターの名前
    count: number; // カウンターのカウント値
  }

  /** 生成したカウンター配列 */
  let counterArray: ICounter[] = [{ deleted: false, name: "new", count: 0 }];
  /** 有効カウンターの配列 */
  $: validCounterArray = counterArray.filter((element) => {return !(element.deleted)});
  /** 有効カウンターのカウンター合計値 */
  $: sum = validCounterArray.reduce((sum, element) => sum + element.count, 0);
  /** 有効カウンターの名前を格納したString配列 */
  $: titleList = validCounterArray.reduce(
    (string, element) => [...string, element.name],
    []
  );
  /** カウンターを増やす関数 */
  function addCounter(): void {
    counterArray = [
      ...counterArray,
      {
        deleted: false,
        name: "new",
        count: 0
      }
    ];
  }
</script>

<h1>サンプル：カウンター作成サイト</h1>

<p>
  <button on:click={addCounter} class="newCounter"
    >新しいカウンターを作成</button
  >
</p>

{#each counterArray as { deleted, name, count }}
  {#if !deleted}
    <Box>
      <input bind:value={name} />
      {#key count}
        <span class="counterCount" in:fly={{ y: -20 }}>{count}</span>
      {/key}

      <Counter bind:deleted bind:count />
    </Box>
  {/if}
{/each}

<div>
  title list: {titleList} <br />

  {#key sum}
    sum of count:<span class="counterCount" in:fly={{ y: -20 }}>{sum}</span>
  {/key}
</div>

<style>
  .newCounter {
    color: #fff;
    background-color: #eb6100;
    cursor: pointer;
  }

  .newCounter:hover {
    color: #fff;
    background: #f56500;
  }

  .counterCount {
    margin: 20px;
    display: inline-block;
    cursor: pointer;
  }
</style>
