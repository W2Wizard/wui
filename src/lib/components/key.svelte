<script lang="ts">
	import type { HTMLAttributes } from "svelte/elements";

	const { children, ...rest } = $props<HTMLAttributes<HTMLElement>>();
</script>

<kbd {...rest}>
	{#if children}
		{@render children()}
	{/if}
</kbd>

<style>
	kbd {
		color: var(--text-03);
		background-color: var(--shade-01);
		border: 1px solid var(--shade-03);
		border-radius: 4px;
		box-shadow:
			0 1px 0px var(--shade-03),
			0 2px 0 0 var(--shade-01) inset;
		display: inline-block;
		font-size: 0.85em;
		font-weight: 700;
		line-height: 1;
		padding: 2px 4px;
		white-space: nowrap;
	}
</style>
