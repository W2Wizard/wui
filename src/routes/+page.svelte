<script>
	import Button from "$lib/components/button.svelte";
	import Checkbox from "$lib/components/checkbox.svelte";
	import DropdownItem from "$lib/components/dropdown/dropdown-item.svelte";
	import Dropdown from "$lib/components/dropdown/dropdown.svelte";
	import Hr from "$lib/components/hr.svelte";
	import Input from "$lib/components/input.svelte";
	import Label from "$lib/components/label.svelte";
	import Search from "$lib/components/search.svelte";
	import Select from "$lib/components/select/select.svelte";
	import Skeleton from "$lib/components/skeleton.svelte";
	import Spinner from "$lib/components/spinner.svelte";
	import Splitplane from "$lib/components/splitplane/Splitplane.svelte";
	import Textarea from "$lib/components/textarea.svelte";
	import Toggle from "$lib/components/toggle.svelte";
	import { Icon, Bars3, Cog6Tooth, Cog } from "svelte-hero-icons";
</script>

<h1>Welcome to your library project</h1>
<p>Create your package using @sveltejs/package and preview/showcase your work with SvelteKit</p>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<div class="grid">
	<Button
		onclick={() => {
			document.documentElement.setAttribute("data-theme", "dark");

			// if (document.documentElement.getAttribute("data-theme") === "dark") {
			// 	document.documentElement.setAttribute("data-theme", "light");
			// } else {
			// }
		}}
	>
		Toggle Theme
	</Button>

	<Button outline>Outline Button</Button>

	<Button href="#">Link Button</Button>

	<Button outline href="#">Outline Link Button</Button>

	<Button outline href="#">
		<Icon src={Bars3} solid size="16px" />
	</Button>

	<Button type="submit">Outline Link Button</Button>

	<Button outline type="submit">Outline Link Button</Button>
</div>

<Hr />

<!-- <Dropdown>
	<svelte:fragment slot="text">Dropdown</svelte:fragment>
	<div>
		<a href="#">Link 1</a>
		<a href="#">Link 2</a>
		<a href="#">Link 3</a>
	</div>
</Dropdown> -->

<Splitplane id="sidebar-view" min="25%" max="75%" pos="33%">
	{#snippet a()}
		<div>Left</div>
	{/snippet}

	{#snippet b()}
		<div>Right</div>
	{/snippet}
</Splitplane>

<DropdownItem>
	<Icon src={Bars3} solid size="16px" />
	Dropdown Item
</DropdownItem>

<Dropdown toggle>
	<DropdownItem href="#">Link 1</DropdownItem>
	<DropdownItem href="#">Link 2</DropdownItem>
	<DropdownItem href="#">Link 3</DropdownItem>
</Dropdown>

<Select>
	<option value="1">Option 1</option>
	<option value="2">Option 2</option>
	<option value="3">Option 3</option>
</Select>

ICON DROPDOWN
<Dropdown toggle>
	{#snippet thumbnail()}
		<span class="center">
			<Icon src={Cog} solid size="24px" />
		</span>
	{/snippet}
	<DropdownItem href="#">Link 1</DropdownItem>
	<DropdownItem href="#">Link 2</DropdownItem>
	<DropdownItem href="#">Link 3</DropdownItem>
</Dropdown>

<Input label="Input" type="text" />

<div class="center" style="gap: 4px; flex-direction: column; align-items: flex-start;">
	<Toggle />
	<Spinner />
	<Checkbox />
	<Textarea />
	<Search onSearch={() => console.log("HAI")} />
	<div class="center" style="gap: 4px; flex-direction: column; align-items: flex-start;">
		<Skeleton width={400} height={75} />
		<Skeleton width={220} height={16} />
		<Skeleton width={200} height={16} />
	</div>
</div>

<form>
	<Label for="input-:0:">Email</Label>
	<Input id="input-:0:" type="email" placeholder="Email..." />

	<Label for="input-:1:">Password</Label>
	<Input id="input-:1:" type="password" placeholder="Password..." />

	<Label for="input-:2:">Number</Label>
	<Input id="input-:2:" type="number" placeholder="Number..." />

	<Label for="input-:3:">Date</Label>
	<Input id="input-:3:" type="date" placeholder="Date..." />

	<Label for="input-:4:">Time</Label>
	<Input id="input-:4:" type="time" placeholder="Time..." />

	<Label for="input-:5:">Datetime</Label>
	<Input id="input-:5:" type="datetime-local" placeholder="Datetime..." />

	<Label for="input-:6:">URL</Label>
	<Input id="input-:6:" type="url" placeholder="URL..." />

	<Label for="input-:7:">Phone</Label>
	<Input id="input-:7:" type="tel" placeholder="Phone..." />

	<Label for="input-:8:">Search</Label>
	<Input id="input-:8:" type="search" placeholder="Search..." />

	<Label for="input-:9:">Color</Label>
	<Input id="input-:9:" type="color" placeholder="Color..." />

	<Label for="input-:10:">Week</Label>
	<Input id="input-:10:" type="week" placeholder="Week..." />

	<Label for="input-:11:">Month</Label>
	<Input id="input-:11:" type="month" placeholder="Month..." />

	<Label for="input-:12:">File</Label>
	<Input id="input-:12:" type="file" placeholder="File..." />
</form>

<style>
	:global(html[data-theme="light"]) {
		& body {
			background-color: white;
		}
	}

	:global(html[data-theme="dark"]) {
		& body {
			background-color: black;
		}
	}

	.grid {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 1rem;
		padding: 1rem;
	}
</style>
