<script>
	export let initialCounter = 0;
	export let maxCounter = 9;
	let contador = initialCounter

	function handleClick () {
		contador++
	}

	$: isEvenOrOdd = contador %2 == 0? 'Is Even': 'Is Odd'
	$: {
		if(contador > maxCounter) {
			console.log('limit contador')
			contador = maxCounter
		}
	}
</script>

<style>
	span {
		color: red;
	}
</style>

<button on:click={handleClick}>Incrementar</button>
<span>{contador}</span>
<span>{isEvenOrOdd}</span>