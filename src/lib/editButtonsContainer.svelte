<script lang="ts">
	import EditButton from "./editButton.svelte";

	export let addTime: (amount: number) => void;
	export let timer: number;
	export let shouldIncrement: boolean;

	const AMOUNT_LIST = [100 * 60 * 60, 100 * 60, 100, 1];
</script>

<div class="w-[495px] flex justify-around">
	{#each AMOUNT_LIST as amount}
		<EditButton amount={shouldIncrement ? amount : -amount} {addTime} {timer} />
	{/each}
</div>
