<script lang="ts">
	import type { HTMLAttributes } from "svelte/elements";

	const { ...rest } = $props<HTMLAttributes<HTMLHRElement>>();
</script>

<hr {...rest} />

<style>
	hr {
		border: none;
		margin: 6px 0px;
		border-bottom: 2px solid var(--border);
		border-left: 2px solid var(--border);
		border-radius: var(--radius);
	}
</style>
