<script lang="ts">
	import { ChevronDown, Icon } from "svelte-hero-icons";
	import type { HTMLSelectAttributes } from "svelte/elements";

	let { selected = "Select...", onSelection, ...rest } = $props<Props>();
	interface Props extends HTMLSelectAttributes {
		selected?: string;
		onSelection?: (option: string) => void;
	}

	let select: HTMLSelectElement;
	let selectText = $state(selected ?? "Select...");

	function setSelected() {
		const value = select.selectedOptions[0]?.value;
		let text = select.selectedOptions[0]?.textContent;
		selectText = text ? text : "Select...";
		selected = value ? value : selectText;
		onSelection && onSelection(selected);
	}

	$effect(setSelected);
</script>

<div class="container">
	<select bind:this={select} on:input={setSelected} {...rest}>
		<option disabled value>Select</option>
		<slot />
	</select>
	<div class="illusion">
		<span>{selectText}</span>
		<Icon src={ChevronDown} size="16px" />
	</div>
</div>

<style>
	div.container {
		border: 1px solid var(--border);
		border-radius: var(--radius);
		position: relative;
		background-color: var(--shade-01);

		& span {
			text-overflow: ellipsis;
			white-space: nowrap;
			overflow: hidden;
			transition: all 0.2s ease-in-out;
		}
	}

	select {
		width: 100%;
		opacity: 0;
		position: absolute;
		z-index: 1;
		top: 0;
		left: 0;
		height: 100%;
		cursor: pointer;
	}

	div.illusion {
		position: relative;
		display: grid;
		gap: 10px;
		grid-auto-flow: column;
		align-items: center;
		/* max-width: 125px; */
		justify-content: space-between;
		padding: 4px 12px;
		border-radius: var(--br);
		height: 100%;
		text-overflow: ellipsis;
		box-shadow: var(--box-shadow);

		& .illusion-input:checked + & {
			border-color: transparent;
		}
	}
</style>
