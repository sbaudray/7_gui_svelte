<script>
	let celsius;

	let fahrenheit;

	function handleCelsiusChange(event) {
		fahrenheit = Math.floor(celsius * (9 / 5) + 32);
	}

	function handleFahrenheitChange(event) {
		celsius = Math.floor((fahrenheit - 32) * (5 / 9));
	}
</script>

<input bind:value={celsius} on:change={handleCelsiusChange} type="number" />
<span>Celsius = </span>
<input bind:value={fahrenheit} on:change={handleFahrenheitChange} type="number" />
<span>Fahrenheit</span>
