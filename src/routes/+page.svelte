<script>
	import Conversation from "$lib/conversation.svelte";
</script>

<div id="container" style="display: flex; flex-direction: column;">
	<header>
		<h1 style="text-align: center;">Anthony Buchholz's Personal Chatbot Representative</h1>
	</header>

	<div id="conversation">
		<Conversation/>
	</div>
</div>

<style>
	#container {
		display: flex;
		flex-direction: column;
		height: 100%;
	}
	#conversation {
		flex-grow: 1;
		display: flex;
		flex-direction: column;
		padding: 2rem;
	}
</style>