<script lang="ts">
	import Timer from "$lib/timer.svelte";
	import ControlButton from "$lib/controlButton.svelte";
	import EditButtonsContainer from "$lib/editButtonsContainer.svelte";

	const FIVE_MINUTES = 5 * 60 * 100;

	let startingTime = FIVE_MINUTES;
	let timer = startingTime;
	let interval: number | null = null;

	$: isStopped = interval === null;

	const resume = () => {
		interval = setInterval(() => {
			timer--;
			if (timer <= 0) {
				timer = 0;
				stop();
			}
		}, 10);
	};

	const stop = () => {
		if (interval === null) return;
		clearInterval(interval);
		interval = null;
	};

	const reset = () => {
		stop();
		timer = startingTime;
	};

	const addTime = (amount: number) => {
		timer += amount;
		if (isStopped) startingTime += amount;
	};
</script>

<main
	class="absolute top-1/2 left-1/2 -translate-y-1/2 -translate-x-1/2 flex flex-col items-center gap-5"
>
	<EditButtonsContainer {addTime} {timer} shouldIncrement={true} />
	<Timer {timer} />
	<EditButtonsContainer {addTime} {timer} shouldIncrement={false} />
	<div class="flex flex-col">
		<ControlButton
			text={timer === startingTime ? "Start" : "Resume"}
			color="text-green-200"
			hoverBackgroundColor="hover:bg-green-200"
			isDisabled={!isStopped || timer === 0}
			onClick={resume}
		/>
		<ControlButton
			text="Stop"
			color="text-red-200"
			hoverBackgroundColor="hover:bg-red-200"
			isDisabled={isStopped}
			onClick={stop}
		/>
		<ControlButton
			text="Reset"
			color="text-red-400"
			hoverBackgroundColor="hover:bg-red-400"
			isDisabled={false}
			onClick={reset}
		/>
	</div>
</main>
