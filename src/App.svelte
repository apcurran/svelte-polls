<script>
	import Header from "./components/Header.svelte";
	import Footer from "./components/Footer.svelte";
	import PollList from "./components/PollList.svelte";
	import CreatePollForm from "./components/CreatePollForm.svelte";
	import Tabs from "./shared/tabs.svelte";

	// Tabs
	let items = ["Current Polls", "Add New Poll"];
	let activeItem = "Current Polls"; // Default

	function tabChange(event) {
		activeItem = event.detail;
	}

	function handleAdd(event) {
		activeItem = "Current Polls";
	}
</script>

<Header />
<main>
	<Tabs items={items} activeItem={activeItem} on:tabChange={tabChange} />
	{#if activeItem === "Current Polls"}
		<PollList />
	{:else if activeItem === "Add New Poll"}
		<CreatePollForm on:add={handleAdd} />
	{/if}
</main>
<Footer />

<style>
	main {
		max-width: 60rem;
		margin: 2rem auto;
	}

	h1 {
		margin-top: 1rem;
		font-size: 1.75rem;
	}

</style>