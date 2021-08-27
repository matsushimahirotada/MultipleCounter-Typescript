<script lang="ts">
  import Counter from "./component/Counter.svelte";
  import Box from "./component/Box.svelte";
  import { fly } from "svelte/transition";

  interface counterObj {
    valid: boolean;
    name: string;
    count: number;
  }

  let counterArray: counterObj[] = [{ valid: true, name: "new", count: 0 }];
  $: validCounterArray = counterArray.filter((ele) => ele.valid);
  $: sum = validCounterArray.reduce((sum, element) => sum + element.count, 0); //各カウンターのカウント合計値

  function addCounter(): void {
    //カウンターを増やす関数
    counterArray = [].concat(counterArray, {
      valid: true,
      name: "new",
      count: 0,
    });
  }
</script>

<!-- svelte-ignore non-top-level-reactive-declaration -->

<h1>サンプル：カウンター作成サイト</h1>

<p>
  <button on:click={addCounter} class="newCounter"
    >新しいカウンターを作成</button
  >
</p>

{#each counterArray as { valid, name, count }}
  {#if valid}
    <Box>
      <input bind:value={name} />
      {#key count}
        <span
          class="counterCount"
          style="display: inline-block"
          in:fly={{ y: -20 }}>{count}</span
        >
      {/key}
      <Counter bind:count bind:valid />
    </Box>
  {/if}
{/each}

<div>
  title list:
  {#each validCounterArray as { name }, i}
    {#if i === validCounterArray.length - 1}
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
