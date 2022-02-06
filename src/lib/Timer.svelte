<script lang="ts">
	let elapsedTime = 0;
	let duration = 10;
	let timerRunning = false;

	function handleResetClick() {
		elapsedTime = 0;
	}

	function runTimer() {
		timerRunning = true;

		return setInterval(() => {
			elapsedTime = Number((elapsedTime + 0.1).toFixed(1));
		}, 100);
	}

	function stopTimer(pid: NodeJS.Timer) {
		timerRunning = false;
		return clearInterval(pid);
	}

	let pid = runTimer();

	$: if (elapsedTime >= duration && timerRunning) {
		stopTimer(pid);
	}

	$: if (elapsedTime < duration && !timerRunning) {
		pid = runTimer();
	}
</script>

<label for="elapsed_time">Elapsed Time:</label>
<meter id="elapsed_time" value={elapsedTime} min={0} max={duration} />
<div>{`${elapsedTime.toFixed(1).toString()}s`}</div>
<label for="duration">Duration:</label>
<input type="range" id="duration" bind:value={duration} min={0} max={20} />
<div><button on:click={handleResetClick}>Reset</button></div>
