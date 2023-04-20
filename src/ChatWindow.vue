<template>
    <div class="chat-header">
        <div class="chat-header-text">Igor InteligentnyInaczej <div class="chat-header-online-dot"> </div></div>
    </div>

    <div class="chat-messages-box">
        <MessagesWindow></MessagesWindow>
    </div>


</template>

<script>
import MessagesWindow from "@/MessagesWindow.vue";

export default {
    name: "ChatWindow",
    components: {MessagesWindow},
}
</script>

<style scoped>
.chat-header {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: nowrap;
    font-weight: 900;
    padding: 10px 0;
    width: 100%;
    text-align: center;
    cursor: default;
    justify-content: space-between;
    border-bottom: 2px solid #f5f5f5;
}

.chat-header-text {
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    padding-left: 20px;
}
.chat-header-online-dot {
    display: block;
    background: #1fb05c;
    height: 8px;
    width: 8px;
    border-radius: 8px;
    margin-left: 5px;
    animation-name: blinking;
    animation-duration: 2.5s;
    animation-iteration-count: infinite;
}

@-moz-keyframes blinking {
    0% {
        opacity: 1;
    }
    50% {
        opacity: 0.5;
    }
    100% {
        opacity: 1;
    }
}
@-webkit-keyframes blinking {
    0% {
        opacity: 1;
    }
    50% {
        opacity: 0.5;
    }
    100% {
        opacity: 1;
    }
}
@-o-keyframes blinking {
    0% {
        opacity: 1;
    }
    50% {
        opacity: 0.5;
    }
    100% {
        opacity: 1;
    }
}
@keyframes blinking {
    0% {
        opacity: 1;
    }
    50% {
        opacity: 0.5;
    }
    100% {
        opacity: 1;
    }
}

</style>