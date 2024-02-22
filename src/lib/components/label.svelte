<script lang="ts">
	import type { HTMLLabelAttributes } from "svelte/elements";

	const { children, ...rest } = $props<HTMLLabelAttributes>();
</script>

<!-- Ignore warning regarding ARIA role -->
<label {...rest} >
	{#if children}
		{@render children()}
	{/if}
</label>

<style>
	label {
		line-height: 1;
		font-weight: 500;
		font-size: .875rem;
	}
</style>
