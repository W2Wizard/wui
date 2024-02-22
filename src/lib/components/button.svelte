<script lang="ts">
	import type { HTMLAttributes, HTMLButtonAttributes } from "svelte/elements";

	type Props = HTMLButtonAttributes &
		HTMLAttributes<HTMLAnchorElement> & {
			/** Only show a outline instead of a full color */
			outline?: boolean;
			/** Show a loading spinner */
			loading?: boolean;
			/** If defined, makes the button an anchor. */
			href?: string;
		};

	let { outline = false, href, loading, children, ...rest } = $props<Props>();
</script>

{#if href}
	<a class:outline class="button transition" {...rest}>
		{@render content()}
	</a>
{:else}
	<button class:outline class="button transition" {...rest}>
		{@render content()}
	</button>
{/if}

{#snippet content()}
	{#if children && !loading}
		{@render children()}
	{:else}
		Loading...
	{/if}
{/snippet}

<style>
	.outline {
		background-color: transparent;
	}

	.button {
		cursor: pointer;
		font-size: 16px;
		color: var(--foreground);
		border: 1px solid var(--border);
		background-color: var(--shade-01);
		padding: 0.35rem;
		white-space: nowrap;

		display: inline-flex;
		place-items: center;
		width: fit-content;

		font-size: 0.875rem;
		line-height: 1.25rem;
		font-weight: normal;
		user-select: none;
		border-radius: calc(var(--radius) - 4px);

		min-height: 1rem;
		min-width: 1rem;

		&:disabled {
			opacity: 0.5;
			cursor: not-allowed;
		}

		&:not(:disabled)[type="submit"] {
			color: var(--primary-fg);
			background-color: var(--primary);
			&:hover {
				background-color: var(--secondary);
			}
		}

		&:hover:not(:disabled) {
			background-color: var(--shade-02);
		}

		&:active:not(:disabled) {
			background-color: var(--shade-03);
		}
	}
</style>
