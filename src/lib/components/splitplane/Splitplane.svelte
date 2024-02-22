<script lang="ts">
	import type { Snippet } from "svelte";
	import { constrain, type Length } from "./utils.js";

	interface Props {
		id?: string;
		type?: "horizontal" | "vertical";
		pos?: Length;
		min?: Length;
		max?: Length;
		disabled?: boolean;
		priority?: "min" | "max";
		onChange?: () => void;
		a: Snippet;
		b: Snippet;
	}

	const {
		id = undefined,
		type = "horizontal",
		pos = "50%",
		min = "0%",
		max = "100%",
		disabled = false,
		priority = "min",
		onChange,
		a,
		b,
	} = $props<Props>();

	// State
	let w = $state(0);
	let h = $state(0);
	let dragging = $state(false);
	let container = $state<HTMLElement>()
	let position = $state<Length>(pos);

	$inspect(w, h);

	$effect(() => {
		if (container) {
			const size = type === 'horizontal' ? w : h;
			position = constrain(container, size, min, max, position, priority);
		}
	});

	function update(x: number, y: number) {
		if (disabled || !container) return;

		const { top, left } = container.getBoundingClientRect();
		const pos_px = type === "horizontal" ? x - left : y - top;
		const size = type === "horizontal" ? w : h;

		position = pos.endsWith("%") ? `${(100 * pos_px) / size}%` : `${pos_px}px`;
		onChange?.();
	}

	function drag(node: HTMLElement, callback: (event: PointerEvent) => void) {
		const pointerdown = (event: PointerEvent) => {
			if (
				(event.pointerType === "mouse" && event.button === 2) ||
				(event.pointerType !== "mouse" && !event.isPrimary)
			)
				return;

			node.setPointerCapture(event.pointerId);

			event.preventDefault();

			dragging = true;

			const onpointerup = () => {
				dragging = false;

				node.setPointerCapture(event.pointerId);

				window.removeEventListener("pointermove", callback, false);
				window.removeEventListener("pointerup", onpointerup, false);
			};

			window.addEventListener("pointermove", callback, false);
			window.addEventListener("pointerup", onpointerup, false);
		};

		node.addEventListener("pointerdown", pointerdown, { capture: true, passive: false });

		return {
			destroy() {
				node.removeEventListener("pointerdown", pointerdown);
			},
		};
	}
</script>

<div
	data-pane={id}
	class="container {type}"
	style="--pos: {position}"
	bind:this={container}
	bind:clientWidth={w}
	bind:clientHeight={h}
>
	<div class="pane">
		{@render a()}
	</div>

	<div class="pane">
		{@render b()}
	</div>

	{#if pos !== "0%" && pos !== "100%"}
		<div
			class="{type} divider"
			class:disabled
			use:drag={(e) => update(e.clientX, e.clientY)}
		/>
	{/if}
</div>

{#if dragging}
	<div class="mousecatcher" />
{/if}

<style>
	.container {
		--sp-thickness: var(--thickness, 8px);
		--sp-color: var(--color, transparent);
		display: grid;
		position: relative;
		width: 100%;
		height: 100%;
	}

	.container.vertical {
		grid-template-rows: var(--pos) 1fr;
	}

	.container.horizontal {
		grid-template-columns: var(--pos) 1fr;
	}

	.pane {
		width: 100%;
		height: 100%;
		overflow: auto;
	}

	.pane > :global(*) {
		width: 100%;
		height: 100%;
		overflow: hidden;
	}

	.mousecatcher {
		position: absolute;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		background: rgba(255, 255, 255, 0.0001);
	}

	.divider {
		position: absolute;
		z-index: 10;
		touch-action: none !important;
		margin-right: calc(-0.5 * var(--sp-thickness));
	}

	.divider::after {
		content: "";
		position: absolute;
		border-left: calc(var(--sp-thickness) * 0.5) solid var(--border, transparent);
		border-top: calc(var(--sp-thickness) * 0.5) solid var(--border, transparent);
	}

	.horizontal > .divider {
		padding: 0 calc(0.5 * var(--sp-thickness));
		width: 0;
		height: 100%;
		cursor: ew-resize;
		left: var(--pos);
		transform: translate(calc(-0.5 * var(--sp-thickness)), 0);
	}

	.horizontal > .divider.disabled {
		cursor: default;
	}

	.horizontal > .divider::after {
		left: 50%;
		top: 0;
		width: 1px;
		height: 100%;
	}

	.vertical > .divider {
		padding: calc(0.5 * var(--sp-thickness)) 0;
		width: 100%;
		height: 0;
		cursor: ns-resize;
		top: var(--pos);
		transform: translate(0, calc(-0.5 * var(--sp-thickness)));
	}

	.vertical > .divider.disabled {
		cursor: default;
	}

	.vertical > .divider::after {
		top: 50%;
		left: 0;
		width: 100%;
		height: 1px;
	}
</style>
