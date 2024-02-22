<script lang="ts">
	import type { HTMLAttributes, HTMLButtonAttributes } from "svelte/elements";

	type Props = HTMLButtonAttributes &
		HTMLAttributes<HTMLAnchorElement> & {
			/** Show a loading spinner */
			loading?: boolean;
			/** If defined, makes the button an anchor. */
			href?: string;
		};

	let { href, loading, children, ...rest } = $props<Props>();
</script>

<li>
	{#if href}
		<a class="element" {...rest}>
			{@render content()}
		</a>
	{:else}
		<button class="element" {...rest}>
			{@render content()}
		</button>
	{/if}
</li>

{#snippet content()}
	{#if children && !loading}
		{@render children()}
	{:else}
		Loading...
	{/if}
{/snippet}

<style>
	li {
		list-style: none;
	}

	.element {
		cursor: pointer;
		font-size: 16px;
		color: var(--foreground);
		background-color: transparent;
		padding: 0.35rem;
		white-space: nowrap;

		display: inline-flex;
		place-items: center;
		width: 100%;
		gap: 0.5rem;

		font-size: 0.875rem;
		line-height: 1.25rem;
		font-weight: normal;
		user-select: none;
		border-radius: calc(var(--radius) - 4px);

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