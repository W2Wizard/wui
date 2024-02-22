<script lang="ts">
	import type { Snippet } from "svelte";
	import { ChevronDown, Icon } from "svelte-hero-icons";
	import type { HTMLDetailsAttributes } from "svelte/elements";

	let { toggle, open, thumbnail, title = "Unknown", children } = $props<Props>();
	interface Props extends HTMLDetailsAttributes {
		toggle?: boolean;
		thumbnail?: Snippet;
	}

	let dropdown: HTMLDetailsElement;
	function windowClick({ target }: MouseEvent) {
		const node = target as Node;
		if (open && dropdown && target && !dropdown.contains(node)) {
			open = false;
		}
	}

	function onLeave() {
		open = toggle ? open : false;
	}

	function onOpen() {
		open = toggle ? open : true;
	}
</script>

<!-- We lose focus on clicking anywhere but this -->
<svelte:window onclick={windowClick} />

<details bind:open bind:this={dropdown} onmouseenter={onOpen} onmouseleave={onLeave}>
	<summary class:border={thumbnail === undefined}>
		{#if thumbnail}
			{@render thumbnail()}
		{:else}
			<div class="content">
				{title}
				<span class="rotate" class:down={open}>
					<Icon src={ChevronDown} size="16px" />
				</span>
			</div>
		{/if}
	</summary>
	<ul class="body">
		{#if children}
			{@render children()}
		{/if}
	</ul>
</details>

<style>
	details {
		& ul.body {
			position: absolute;
			z-index: 99999;
			padding: 0.25rem;
			z-index: 99999;
			list-style: none;
			width: fit-content;
			border-radius: var(--radius);
			border: 1px solid var(--border);
			background-color: var(--shade-01);
			min-width: 200px;
		}

		& summary {
			padding: 0.25rem;
			cursor: pointer;
			margin-bottom: 0.25rem;
			border-radius: var(--radius);

			&::marker {
				content: "";
			}

			&:hover {
				user-select: none;
			}

			&.border {
				border: 1px solid var(--border);
			}

			& div.content {
				display: flex;
				align-items: center;
				justify-content: space-between;
				gap: 4px;
				padding-inline: 0.5rem;
			}

			& .content span.rotate {
				display: flex;
				transform: rotate(-90deg);
				transform-origin: center;
				transition: transform 0.1s ease-in-out;

				&.down {
					transform: rotate(0deg);
				}
			}
		}
	}

	/* details {
		z-index: 9999;
		border-radius: var(--br);
	}

	details summary::-webkit-details-marker {
		display: none;
	}

	div.body {
		position: absolute;
		padding: 8px 4px;
		z-index: 99999;
	}

	summary {
		cursor: pointer;

		&::marker {
			content: "";
		}

		&:hover {
			user-select: none;
		}

		& div.content {
			display: flex;
			align-items: center;
			gap: 4px;
		}

		& .content span.rotate {
			display: flex;
			transform: rotate(-90deg);
			transform-origin: center;
			transition: transform 0.1s ease-in-out;

			&.down {
				transform: rotate(0deg);
			}
		}
	} */
</style>
