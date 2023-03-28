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
        <div class="spacer"></div>
        {#each $chatHistory as message}
            <ChatMessage 
            messageText={message.text} 
            messageTime={message.time} 
            messageUser={message.user}
            />
        {/each}
    </div>
    <form>
        <input 
        type="text"
        name="messageText"
        class="message-input"
        >
        <button 
        type="submit" 
        on:click={sendMessage} 
        class="send-btn"
        >Send</button>
    </form>
</div>

<style>
    /* make button rounded style */
    .main-container {
        display: flex;
        flex-direction: column;
        height: 95vh;
        align-items: center;
    }

    .spacer {
        height: 75vh;
    }
    .chat-box {
        display: flex;
        width: 30%;
        flex-direction: column;
        overflow: auto;
        flex-grow: 1;
        align-items: flex-end;
    }

    .message-input {
        border-radius: 1rem;
        font-size: medium;
        background-color: #3b4248;
        color: white;
        width: 50rem;
        height: 50px;
    }
    .send-btn {
        border-radius: 5rem;
        width: 100px;
        height: 50px;
        background-color: #326b00;
        color: white;
        font-size: 1.5rem;
        border: none;
    }
</style>