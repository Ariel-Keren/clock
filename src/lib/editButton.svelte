<script lang="ts">
	export let amount: number;
	export let addTime: (amount: number) => void;
	export let timer: number;

	const addAmount = () => {
		if (timer < -amount) return;
		addTime(amount);
	};
</script>

<button on:click={addAmount} class="text-gray-400 text-5xl">{amount >= 0 ? "+" : "-"}</button>
