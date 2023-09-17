<script lang="ts">
	export let text: string;
	export let color: string;
	export let hoverBackgroundColor: string;
	export let isDisabled: boolean;
	export let onClick: () => void;
</script>

<button
	on:click={onClick}
	disabled={isDisabled}
	class={`${
		isDisabled ? "text-gray-500" : `${color} ${hoverBackgroundColor} hover:text-black`
	} bg-none text-2xl font-medium uppercase h-12 w-32 rounded transition-colors`}>{text}</button
>
