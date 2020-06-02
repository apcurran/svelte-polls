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
		const poll = event.detail;

		polls = [poll, ...polls];
		console.log(polls);

		activeItem = "Current Polls";
	}

	function handleVote(event) {
		const { id, option } = event.detail;

		let copiedPolls = [...polls];
		let upvotedPoll = copiedPolls.find(poll => poll.id === id);

		if (option === "a") {
			upvotedPoll.votesA++;
		} else if (option === "b") {
			upvotedPoll.votesB++;
		}

		polls = copiedPolls;
	}

</script>

<Header />
<main>
	<Tabs items={items} activeItem={activeItem} on:tabChange={tabChange} />
	{#if activeItem === "Current Polls"}
		<PollList on:vote={handleVote} />
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