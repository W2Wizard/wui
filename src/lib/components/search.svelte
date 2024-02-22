<script lang="ts">
	import Kbd from "./key.svelte";
	import { Icon, MagnifyingGlass } from "svelte-hero-icons";
	import type { HTMLBaseAttributes } from "svelte/elements";

	interface Props extends HTMLBaseAttributes {
		onSearch: (value: string) => void;
	}

	const searchKey = "s";
	let value = $state("");
	let input = $state<HTMLInputElement>();
	const { onSearch, children, ...rest } = $props<Props>();

	function captureFocus(e: KeyboardEvent) {
		if (
			e.key === searchKey &&
			!e.ctrlKey &&
			!e.shiftKey &&
			!e.altKey &&
			!e.metaKey &&
			document.activeElement === document.body
		) {
			e.preventDefault();
			input?.focus();
		}

		if (e.key === "Escape") {
			input?.blur();
			value = "";
		}

		if (e.key === "Enter" && value.length > 0) {
			onSearch(value);
		}
	}
</script>

<svelte:window on:keydown={captureFocus} />

<search class="center transition" {...rest}>
	<Icon src={MagnifyingGlass} size="16px" />
	<div class="container">
		<input
			bind:this={input}
			bind:value
			title="Search the world..."
			name="search"
			autocomplete="off"
		/>
		<span class:hidden={value.length > 0}>
			Press <Kbd>{searchKey}</Kbd> to search
		</span>
	</div>
</search>

<style>
	.hidden {
		opacity: 0 !important;
	}

	input {
		flex: 1;
		border: none;
		outline: none;
		width: 100%;
		height: 20px;
		color: var(--foreground);
		padding-left: 4px;
		background: transparent;
	}

	div.container {
		flex: 1;
		position: relative;

		& span {
			position: absolute;
			display: flex;
			align-items: center;
			gap: 4px;
			top: 1px;
			left: 6px;
			pointer-events: none;
			user-select: none;
			color: var(--text-04);
			opacity: 1;
			height: 100%;
			font-size: 0.8rem;

			&.hidden {
				opacity: 0;
			}
		}
	}

	search.center {
		border-radius: var(--radius);
		border: 1px solid var(--border);
		padding: 4px 12px;
		min-width: 12rem;
		width: 15rem;
		flex: 1 1 auto;
		box-shadow: var(--box-shadow);

		@media only screen and (max-width: 768px) {
			& kbd {
				display: none;
			}
		}
	}
</style>
