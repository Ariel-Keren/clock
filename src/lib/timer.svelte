<script lang="ts">
	export let timer: number;

	const padNumber = (number: number) => number.toString().padStart(2, "0");

	$: hours = padNumber(Math.floor(timer / 100 / 60 / 60));
	$: minutes = padNumber(Math.floor(timer / 100 / 60) % 60);
	$: seconds = padNumber(Math.floor((timer / 100) % 60));
	$: centiseconds = padNumber(Math.floor(timer % 100));

	$: formattedTimer = `${hours}:${minutes}:${seconds}.${centiseconds}`;
</script>

<span class="text-gray-300 text-8xl select-none">{formattedTimer}</span>
