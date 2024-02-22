<script lang="ts">
	import type { HTMLInputAttributes } from "svelte/elements";

	const { id, title, required, ...rest } = $props<HTMLInputAttributes>();
</script>

<!-- HTML -->

<div class="container transition">
	<span class="parent">
		<input {id} on:input on:keydown on:change {...rest} />
		<!-- {#if inputType == "url"}
			<Url on:click={() => copyToClipboard()} />
		{:else if inputType == "password"}
			<Password on:toggle={(e) => togglePassword(e.detail.hidden)} />
		{/if} -->
	</span>
</div>

<!-- Styling -->

<style>
	.container {
		display: grid;
	}

	.parent {
		display: flex;
		color: var(--foreground);
		/* height: 100%; */

		& input {
			color: inherit;
			appearance: none;
			border: none;
			background: none;
			outline: none;
			padding: 0.25rem;
			width: 100%;
			border-radius: var(--br);

			&::-webkit-slider-thumb {
				display: none;
			}

			/* WTF */
			&::-webkit-calendar-picker-indicator {
				color: var(--foreground-color);
			}

			&::file-selector-button {
				padding: 0.25rem;
				/* appearance: none;
				padding: 0.25rem;
				background-color: var(--shade-02);
				cursor: pointer;
				border-radius: var(--radius);
				box-shadow: var(--box-shadow);
				border: 1px solid black;
				color: var(--foreground); */
			}

			&[type="password"]::-ms-reveal {
				display: none;
			}

			&[type="search"] {
				/* clears the ‘X’ from Internet Explorer */
				&::-ms-clear {
					display: none;
					height: 0;
					width: 0;
				}

				&::-ms-reveal {
					display: none;
					height: 0;
					width: 0;
				}
				/* clears the ‘X’ from Chrome */
				&::-webkit-search-decoration,
				&::-webkit-search-cancel-button,
				&::-webkit-search-results-button,
				&::-webkit-search-results-decoration {
					display: none;
				}
			}

			&[type="color"] {
				padding: 4px;
			}

			&[type="range"] {
				box-shadow: none;
			}

			&:disabled {
				color: var(--text-03);
				cursor: not-allowed;
			}
		}

		/* height: inherit; */

		border-radius: calc(var(--radius) - 4px);
		background-color: var(--shade-01);
		border: 1px solid var(--border);
		box-shadow: var(--box-shadow);

		width: 100%;

		&:has(input:disabled) {
			background-color: var(--shade-02);
		}

		& > input[type="range"] {
			display: none;

			/* Show the custom slider thumb */
			&::-moz-range-thumb {
				display: block;
				width: 1em;
				height: 1em;
				border-radius: 50%;
				background-color: var(--primary);
				border: 1px solid var(--border-color);
				box-shadow: var(--box-shadow);
				cursor: pointer;
			}
		}
	}
</style>
