<script>
	let count = 0;
</script>

<input disabled bind:value={count} type="text" />
<button on:click={() => (count += 1)}>Count</button>
