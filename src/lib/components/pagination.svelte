<!-- <script lang="ts">
	import { page } from "$app/stores";
	import { onMount } from "svelte";
	import {
		ChevronDoubleLeft,
		ChevronDoubleRight,
		ChevronLeft,
		ChevronRight,
		Icon
	} from "svelte-hero-icons";

	export let pages = 0;
	export let current = 0;

	// Pages start at 0 so we subtract 1
	$: prevDisabled = current === 0 || pages === 0;
	$: nextDisabled = current === pages - 1 || pages === 0;
	$: current = Math.min(Math.max(current, 0), pages - 1);
	$: current = isNaN(current) || pages === 0 ? 0 : current; // HACK: Fucking garbage

	onMount(() => {
		const params = $page.url.searchParams;
		if (params.has("page")) {
			let page = parseInt(params.get("page") ?? "0");
			if (page >= 0 && page <= pages) {
				current = page;
			}
		}
	});
</script>

<menu role="navigation" aria-label="Pagination">
	<li>
		<a
			class="object round-left"
			href="?page={current}"
			on:click={() => current--}
			aria-disabled={prevDisabled}
			inert={prevDisabled}
		>
			<Icon src={ChevronLeft} size="16" />
		</a>
		<a
			class="object skip"
			href="?page={0}"
			aria-disabled={prevDisabled}
			inert={prevDisabled}
			on:click={() => (current = 0)}
		>
			<Icon src={ChevronDoubleLeft} size="16" />
		</a>
	</li>
	<li class="count">
		<p class="object">{current}</p>
	</li>
	<li>
		<a
			class="object"
			href="?page={pages - 1}"
			aria-disabled={nextDisabled}
			inert={nextDisabled}
			on:click={() => (current = pages - 1)}
		>
			<Icon src={ChevronDoubleRight} size="16" />
		</a>
		<a
			class="object round-right"
			href="?page={current}"
			on:click={() => current++}
			aria-disabled={nextDisabled}
			inert={nextDisabled}
		>
			<Icon src={ChevronRight} size="16" />
		</a>
	</li>
</menu>

<style>
	menu {
		display: inline-flex;
		align-items: center;
		list-style: none;
		padding: 0;
		margin: 0;

		& li.count {
			flex: 1;
		}

		& li:first-child,
		li:last-child {
			display: flex;
			align-items: center;
		}
	}

	[aria-disabled="true"],
	[inert] {
		cursor: not-allowed;
		opacity: 0.5;
	}

	.object {
		display: flex;
		align-items: center;
		justify-content: center;
		background-color: var(--shade-01);
		border: 1px solid var(--border-color);
		color: var(--text-1);
		padding: 8px;
		margin: 0;
		cursor: pointer;

		&:is(p) {
			line-height: 1;
			font-size: 16px;
			border-left: none;
			border-right: none;
			min-width: 32px;
		}

		&.round-left {
			border-right: none;
			border-top-left-radius: var(--br);
			border-bottom-left-radius: var(--br);
		}

		&.round-right {
			border-left: none;
			border-top-right-radius: var(--br);
			border-bottom-right-radius: var(--br);
		}
	}
</style> -->
