<script>
	import { fade } from "svelte/transition";
	import Checkmark from "$lib/icons/checkmark.svelte";

	let checked = $state(false);
</script>

<button
	class="center transition"
	onclick={() => (checked = !checked)}
	role="checkbox"
	aria-checked={checked}
>
	{#if checked}
		<span transition:fade={{ duration: 50 }}>
			<Checkmark />
		</span>
	{/if}
</button>

<style>
	button {
		border: 1px solid var(--border);
		border-radius: calc(var(--radius) - 4px);
		background-color: transparent;
		cursor: pointer;

		width: 1rem;
		height: 1rem;

		&[aria-checked="true"] {
			background-color: var(--primary);
			border-color: var(--primary);
		}
	}

	span {
		display: flex;
		align-items: center;
		justify-content: center;
		pointer-events: none;
		color: var(--primary-fg);
	}
</style>
