<script lang="ts">
	import type { HTMLAttributes } from "svelte/elements";

	interface Props extends HTMLAttributes<HTMLDivElement> {
		strokeWidth?: string | number;
		radius?: string | number;
	}

	const { strokeWidth = 5, radius = 20, ...rest } = $props<Props>();
</script>

<div {...rest}>
	<svg viewBox="0 0 50 50">
		<circle cx="25" cy="25" r={radius} fill="none" stroke-width={strokeWidth} />
	</svg>
</div>

<style>
	div {
		display: block;
		z-index: 9999;
		width: 42px;
		height: 42px;

		& svg {
			user-select: none;
			pointer-events: none;
			animation: rotate 2s linear infinite;

			& circle {
				stroke: var(--primary);
				stroke-linecap: round;
				animation: dash 1.5s ease-in-out infinite;
			}
		}
	}

	@keyframes rotate {
		100% {
			transform: rotate(360deg);
		}
	}

	@keyframes dash {
		0% {
			stroke-dasharray: 1, 150;
			stroke-dashoffset: 0;
		}
		50% {
			stroke-dasharray: 90, 150;
			stroke-dashoffset: -35;
		}
		100% {
			stroke-dasharray: 90, 150;
			stroke-dashoffset: -124;
		}
	}
</style>
