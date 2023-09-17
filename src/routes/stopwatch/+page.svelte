<script lang="ts">
	import Timer from "$lib/timer.svelte";
	import ControlButton from "$lib/controlButton.svelte";
	import SetModal from "$lib/setModal.svelte";

	const FIVE_MINUTES = 5 * 60 * 100;

	let endingTime = FIVE_MINUTES;
	let timer = 0;
	let interval: number | null = null;
	let isModalShown = false;

	$: isStopped = interval === null;

	const resume = () => {
		interval = setInterval(() => {
			timer++;
			if (timer >= endingTime) {
				timer = endingTime;
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
		timer = 0;
	};

	const addTime = (amount: number) => {
		endingTime += amount;
	};

	const showModal = () => {
		isModalShown = true;
	};

	const hideModal = () => {
		isModalShown = false;
	};
</script>

<main
	class="absolute top-1/2 left-1/2 -translate-y-1/2 -translate-x-1/2 flex flex-col items-center gap-5"
>
	<ControlButton
		text="Set"
		color="text-blue-200"
		hoverBackgroundColor="hover:bg-blue-200"
		isDisabled={false}
		onClick={showModal}
	/>
	<Timer {timer} />
	<div class="flex flex-col">
		<ControlButton
			text={timer === 0 ? "Start" : "Resume"}
			color="text-green-200"
			hoverBackgroundColor="hover:bg-green-200"
			isDisabled={!isStopped || timer === endingTime}
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
			isDisabled={timer === 0}
			onClick={reset}
		/>
	</div>
</main>
{#if isModalShown}
	<SetModal {endingTime} {addTime} {hideModal} />
{/if}
