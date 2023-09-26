<script>
	import Dialogbox from "./dialogbox.svelte";

    let conversation = [{
            type: "bot",
            message: "Hello, I am Anthony Buchholz's personal chatbot representative. I have been fed his resume and will do my best to answer any questions about him. Keep in mind, not all answers are guaranteed to have correct information."
        }, {
            type: "bot",
            message: "What questions do you have for me?"
        }];

    let userInput = "";

    async function submit() {
        conversation = [...conversation, {type: "user", message: userInput}];
        const request = fetch("/", {
            method: "POST",
            body: JSON.stringify({
                userInput: userInput
            })
        });
        userInput = "";
        try {
            const botResponse = {type: "bot", message: "Loading..."};
            conversation = [...conversation, botResponse];
            const response = await request;
            if (response.status !== 200) {
                botResponse.message = "I'm sorry something went wrong coming up with an answer, try again.";
            }
            const responseText = await response.text();
            botResponse.message = responseText;
            conversation = conversation;
        } catch {
            const botResponse = {type: "bot", message: "I'm sorry something went wrong coming up with an answer, try again."};
            conversation = [...conversation, botResponse];
        }
    }
</script>

<div id="container">
    <div id="dialogContainer">
        {#each conversation as message}
            <div class="message">
                <Dialogbox message={message.message} type={message.type}/>
            </div>
        {/each}
    </div>
    <form id="inputContainer" on:submit={submit}>
        <input type="text" name="userInput" id="conversationInput" bind:value={userInput}>
        <button type="submit">Send</button>
    </form>
</div>

<style>
    .message{
        padding: 0 1rem 1rem 0;
        clear: both;
    }
    #container {
        border: 1px solid grey;
        height: 100%;
        padding: 1rem;
        display: flex;
        border-radius: 5px;
        flex-direction: column;
    }
	#conversationInput {
		border-radius: 5px;
        width: 100%;
        padding-left: 0.5rem;
	}
	#inputContainer {
        display: flex;
        flex-direction: row;
        gap: 1rem;
	}
    button {
        padding: 0.5rem;
        border-radius: 0.5rem;
        background-color: blue;
        color: white;
    }
    #dialogContainer {
        flex-grow: 1;
        overflow: auto;
        height: 500px;
    }
</style>