<script lang="ts">
	enum FlightType {
		oneWayFlight,
		returnFlight
	}

	let flightType = FlightType.oneWayFlight;

	const INITIAL_DATE = '2014-03-27';

	let startDate = INITIAL_DATE;
	let endDate = INITIAL_DATE;

	let invalidStartDate = false;
	let invalidEndDate = false;

	let successMessage: string;

	$: invalidReturnFlight =
		flightType === FlightType.returnFlight && new Date(endDate) > new Date(startDate);

	function handleStartDateBlur() {
		invalidStartDate = isNaN(new Date(startDate).getTime());
	}

	function handleEndDateBlur() {
		invalidEndDate = isNaN(new Date(endDate).getTime());
	}

	function handleSubmit(event: SubmitEvent) {
		event.preventDefault();

		switch (flightType) {
			case FlightType.oneWayFlight:
				successMessage = `You have booked a one-way flight on ${startDate}`;
				break;
			case FlightType.returnFlight:
				successMessage = `You have booked a return flight departing on ${startDate} and returning on ${endDate}.`;
				break;
		}
	}
</script>

<form on:submit={handleSubmit}>
	<select bind:value={flightType}>
		<option value={FlightType.oneWayFlight}>one-way flight</option>
		<option value={FlightType.returnFlight}>return flight</option>
	</select>
	<div>
		<input
			bind:value={startDate}
			aria-invalid={invalidStartDate || null}
			aria-errormessage="startDateError"
			on:blur={handleStartDateBlur}
		/>
		<div id="startDateError" class="errorMessage">Invalid date entered</div>
	</div>
	<div>
		<input
			bind:value={endDate}
			disabled={flightType !== FlightType.returnFlight}
			aria-invalid={invalidEndDate || null}
			aria-errormessage="endDateError"
			on:blur={handleEndDateBlur}
		/>
		<div id="endDateError" class="errorMessage">Invalid date entered</div>
	</div>
	<button type="submit" disabled={invalidReturnFlight || invalidStartDate || invalidEndDate}>
		Book
	</button>
</form>
{#if successMessage}
	<div role="alert">{successMessage}</div>
{/if}

<style>
	form {
		display: flex;
		flex-direction: column;
		max-width: 250px;
		gap: 20px;
	}

	[aria-invalid] {
		/* outline: 1px solid red; */
		background: red;
	}

	[aria-invalid] ~ .errorMessage {
		visibility: visible;
	}

	.errorMessage {
		visibility: hidden;
	}
</style>
