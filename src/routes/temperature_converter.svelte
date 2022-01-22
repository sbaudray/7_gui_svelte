<script context="module" lang="ts">
	export const prerender = true;
</script>

<script lang="ts">
	import TemperatureConverter from '$lib/TemperatureConverter.svelte';
</script>

<svelte:head>
	<title>Temperature Converter</title>
</svelte:head>

<TemperatureConverter />
