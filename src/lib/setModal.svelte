<script lang="ts">
	import Timer from "$lib/timer.svelte";
	import ControlButton from "./controlButton.svelte";
	import EditButtonsContainer from "./editButtonsContainer.svelte";

	export let endingTime: number;
	export let addTime: (amount: number) => void;
	export let hideModal: () => void;
</script>

<div
	class="absolute top-0 left-0 h-screen w-screen backdrop-brightness-75 flex justify-center items-center"
>
	<div class="h-1/4 w-1/2 bg-gray-950 rounded flex flex-col justify-around items-center">
		<div>
			<EditButtonsContainer {addTime} timer={endingTime} shouldIncrement={true} />
			<Timer timer={endingTime} />
			<EditButtonsContainer {addTime} timer={endingTime} shouldIncrement={false} />
		</div>
		<ControlButton
			text="Close"
			color="text-red-200"
			hoverBackgroundColor="hover:bg-red-200"
			isDisabled={false}
			onClick={hideModal}
		/>
	</div>
</div>
