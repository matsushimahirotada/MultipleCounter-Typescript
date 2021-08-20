<script lang="ts">

    import Counter from './Counter.svelte';
	import Box from './Box.svelte';

	$:CounterArray = [{id:0,name:'new',count:0}];
	$:Sum = 0;

	function addCounter():void{
		CounterArray[CounterArray.length] = {id:CounterArray.length,name:'new',count:0}
		Sum=SumofCount()
	}


	function deleteCounter(event):void{
		const id:number = event.detail.order
		const firsthalfofArray:{id:number,name:string,count:number}[] = CounterArray.slice(0,id)
		const letterhalfofArray:{id:number,name:string,count:number}[] = CounterArray.slice(id+1)
		
		for (const entry of letterhalfofArray){
			firsthalfofArray[firsthalfofArray.length] = {id:firsthalfofArray.length,name:entry.name,count:entry.count};
		}

		CounterArray = firsthalfofArray;
		Sum=SumofCount();

	}

	function updateCount(event):void{
		const id:number = event.detail.Id;
		const count:number = event.detail.Count;
		
		CounterArray[id] = {id:id,name:CounterArray[id].name,count:count};
		Sum = SumofCount();

	}

	function SumofCount():number{
		let sum:number=0;

		for(const entry of CounterArray){
			sum = sum + entry.count;
		}

		return sum;
	}

</script>

<!-- svelte-ignore non-top-level-reactive-declaration -->

<h1>カウンター</h1>

<button on:click={addCounter}>
	新しいカウンターを作成
</button>

{#each CounterArray as counter(counter.id)}
	<Box>
		<input bind:value={counter.name}>
		{counter.count}
		<Counter on:deleteorder={deleteCounter}
		on:updatecountorder={updateCount}
		id = {counter.id}
		/>
	</Box>
{/each}

	<div>title list:

		{#each CounterArray as {name}}
			{name},
		{/each}
	</div>

	<div>
		sum of count:{Sum}
	</div>
<style>
</style>