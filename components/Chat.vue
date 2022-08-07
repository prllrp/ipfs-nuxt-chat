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
                <div v-for="message in messages" v-bind:key="message"  class="chat-body-message">
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
    data() {
        return {
            message: '',
            messages: messages,
            title: 'Chat'
        };
    },
    methods: {
        sendMessage() {
            node.pubsub.publish('pubsub-test', new TextEncoder().encode({id: node.id(), time: new Date().getTime(), msg: this.message}))
            messages.push({
                text: this.message,
                time: new Date().toLocaleTimeString()
            });
            this.message = '';
        }
    },
    props: {
        node: {
            type: Object,
            required: true
        }
    },
    onMount(){
        node.pubsub.subscribe('pubsub-test', (msg) => {
            console.log(msg)
            messages.push({
                text: msg.data.toString(),
                time: new Date().toLocaleTimeString()
            });
        })
    }
}

</script>

<style>

</style>