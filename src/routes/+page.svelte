<script lang="ts">
	const padNumber = (number: number) => number.toString().padStart(2, "0");

	let hours = new Date().getHours();
	let minutes = new Date().getMinutes();
	let seconds = new Date().getSeconds();

	$: time = `${padNumber(hours)}:${padNumber(minutes)}:${padNumber(seconds)}`;

	setInterval(() => {
		hours = new Date().getHours();
		minutes = new Date().getMinutes();
		seconds = new Date().getSeconds();
	}, 1000);
</script>

<span class="absolute top-1/2 left-1/2 -translate-y-1/2 -translate-x-1/2 text-gray-300 text-8xl"
	>{time}</span
>
