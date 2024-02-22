<script lang="ts">
	import type { HTMLAttributes } from "svelte/elements";

	interface Props extends HTMLAttributes<HTMLDivElement> {
		width?: number | number;
		height?: number | number;
	}

	const { width = 200, height = 200, ...rest } = $props<Props>();
</script>

<div style="width: {width}px; height: {height}px" {...rest} />

<style>
	div {
		border-radius: var(--radius);
		background-color: var(--shade-02);
		animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
	}

	@keyframes pulse {
		50% {
			opacity: 0.5;
		}
	}
</style>
