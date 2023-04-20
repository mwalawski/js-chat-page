<template>
    <input v-on:keyup.enter="send()" placeholder="Aa" class="chat-input-text" v-model="newMessage">
    <font-awesome-icon icon="fa-solid fa-paper-plane" class="send-msg-button" @click="send()" />
</template>

<script>

export default {
    name: "ChatInput",
    data() {
        return {
            newMessage: '',
        }
    },
    methods: {
        send(){
            if(this.newMessage.length > 0){
                this.$emit('addMessage', this.newMessage);
                this.newMessage = '';
            }
        },
    },
    emits :{
        addMessage: null,
    }
}
</script>

<style scoped>

.chat-input-text {
    font-family: 'Roboto';
    font-size: 1em;
    width: 100%;
    border: none;
    background: #f3f3f3;
    margin: 0 10px;
    padding: 5px 15px;
    color: #444;
    border-radius: 15px;
    box-sizing: border-box;
}

.send-msg-button {
    transition-duration: 0.2s;
}

.send-msg-button:hover {
    color: #0084ff;
}

</style>