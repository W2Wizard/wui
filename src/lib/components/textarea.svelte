<script lang="ts">
	import type { HTMLTextareaAttributes } from "svelte/elements";

	const { type = "vertical", ...rest } = $props<Props>();
	interface Props extends HTMLTextareaAttributes {
		type?: "horizontal" | "vertical";
	}
</script>

<textarea style="resize: {type};" placeholder="Type your message here." {...rest} />

<style>
	.vertical {
		resize: vertical;
	}

	.horizontal {
		resize: horizontal;
	}

	textarea {
		display: block;
		border-radius: var(--radius);
		border: 1px solid var(--border);
		background: transparent;
		color: var(--fg);
		padding: 8px;
		outline: none;
		box-shadow: var(--box-shadow);
		width: 100%;
		min-height: 128px;
	}
</style>
