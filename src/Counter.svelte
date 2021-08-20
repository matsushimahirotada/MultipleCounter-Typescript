<script lang="ts">

	import { createEventDispatcher } from 'svelte';

    const dispatch:any = createEventDispatcher();
    const dispatch2:any = createEventDispatcher();

    export let id: number;
	let count:number=0;

	function CounterInc():void{
		count +=1
        dispatch2('updatecountorder',{Id:id,Count:count});
	}

	function CounterDec():void{
		if (count>0){
			count -=1
            dispatch2('updatecountorder',{Id:id,Count:count});
		}
	}

	function Counterreset():void{
		count=0
        dispatch2('updatecountorder',{Id:id,Count:count});
	}
    

    function deleteCounter():void{
        dispatch('deleteorder',{order:id});
    }

</script>

<!-- svelte-ignore non-top-level-reactive-declaration -->
	
    <button on:click={CounterInc}>
        +
    </button>
	
    <button on:click={CounterDec}>
        -
    </button>
	
    <button on:click={Counterreset}>
        0
    </button>

    <button on:click={deleteCounter}>
        X
    </button>

<style>
</style>