<template>
    <div class="chat">
        <div class="chat-header">
            <div class="chat-header-title">
                <h3>{{ title }}</h3>
            </div>
            <div class="chat-header-buttons">
                <button class="btn btn-primary" @click="sendMessage">Send</button>
            </div>
        </div>
        <div class="chat-body">
            <div class="chat-body-messages">
                <div v-for="message in messages" class="chat-body-message">
                    <div class="chat-body-message-text">
                        {{ message.text }}
                    </div>
                    <div class="chat-body-message-time">
                        {{ message.time }}
                    </div>
                </div>
            </div>
        </div>
        <div class="chat-footer">
            <div class="chat-footer-input">
                <input type="text" v-model="message" @keyup.enter="sendMessage" />
            </div>
        </div>
    </div>
</template>

<script>
const messages = [];
export default {

}
</script>

<style>

</style>