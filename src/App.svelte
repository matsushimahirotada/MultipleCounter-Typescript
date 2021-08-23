<script lang="ts">
  import Counter from "./component/Counter.svelte";
  import Box from "./component/Box.svelte";
  import { fly } from "svelte/transition";
import { current_component, prevent_default } from "svelte/internal";

  let counterArray = [
    {
      //カウンター
      id: 0, //カウンターのid
      name: "new", //カウンターの名前
      count: 0 //カウンターのカウント値
    }
  ];

  let sum = 0; //各カウンターのカウント合計値

  function addCounter(): void {
    //カウンターを増やす関数
	const result = [].concat(counterArray,{id:counterArray.length,name:"new",count:0});
    $:sum = counterArray.reduce((prevent_default,current_component,indexedDB,array)=>{
		return pre + current.count}); //各カウンターのカウント合計値更新

  }

  function deleteCounter(event): void { //カウンターを減らす関数
    const id: number = event.detail.order; //deleteされたカウンターのidを取得
	
    sum = SumofCount(); //各カウンターのカウント合計値更新
  }

  function updateCount(event): void {
    const id: number = event.detail.Id; //カウント値が変動したカウンターのidを取得
    const count: number = event.detail.Count; //最新のカウント値

    CounterArray[id] = { id: id, name: CounterArray[id].name, count: count }; //カウント値を更新
    sum = SumofCount(); //各カウンターのカウント合計値更新
  }

  function SumofCount(): number {
    //各カウンターのカウント合計値を返す関数

    let sum: number = 0;

    for (const entry of CounterArray) {
      sum = sum + entry.count;
    }

    return sum;
  }
</script>

<!-- svelte-ignore non-top-level-reactive-declaration -->

<h1>サンプル：カウンター作成サイト</h1>

<p>
  <button on:click={addCounter} class="newcounter">新しいカウンターを作成</button>
</p>

{#each CounterArray as counter (counter.id)}
  <Box>
    <input bind:value={counter.name} />

    {#key counter.count}
      <span
        class="Countercount"
        style="display: inline-block"
        in:fly={{ y: -20 }}>{counter.count}</span>
    {/key}

    <Counter on:deleteorder={deleteCounter} on:updatecountorder={updateCount} id={counter.id}/>
  </Box>
{/each}

<div>
  title list:
  {#each CounterArray as { id, name }}
    {#if id == CounterArray.length - 1}
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
      in:fly={{ y: -20 }}>{sum}</span>
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
