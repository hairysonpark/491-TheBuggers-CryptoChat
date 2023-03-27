<script>
    import { setContext } from 'svelte';
    import { writable } from 'svelte/store';
    import ChatMessage from './ChatMessage.svelte';
    let chatHistory = writable([]);
    setContext('chatHistory', chatHistory);

    let getMessage = () => {
        let message = {
            text: document.querySelector('input[name=messageText]').value,
            time: "12:00 pm",
            user: "Joe"
        }
        return message;
    }

    let sendMessage = () => {
        let message = getMessage();
        chatHistory.update((messages) => {
            return [...messages, message];
        });
    }



</script>

<div class="main-container">
    <div class="chat-box">
        <!-- Chat messages will be rendered here -->
        {#each $chatHistory as message}
            <ChatMessage messageText={message.text} messageTime={message.time} messageUser={message.user} />
        {/each}
    </div>
    <form>
        <input type="text" name="messageText">
        <button type="submit" on:click={sendMessage}>Send</button>
    </form>
</div>

<style>

</style>