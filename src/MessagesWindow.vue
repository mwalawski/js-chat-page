<template>
    <div v-for="message in messages" :key="message.id" class="msg-box-line">
        <div v-if="message.isMy" class="msg-box-line-my">
            <div class="msg-box-message-my">
                {{ message.text }}
            </div>
        </div>
        <div v-else class="msg-box-line-other">
            <div v-if="message.isWarning" class="msg-box-message-other msg-box-message-other-warning">
                    {{ message.text }}
            </div>
            <div v-else class="msg-box-message-other">
                {{ message.text }}
            </div>
        </div>
    </div>
    <div v-if="isBotTyping" class="msg-box-line">
        <div class="msg-box-message-other">
            <div class="typing">
            <div class="dot">•</div>
            <div class="dot">•</div>
            <div class="dot">•</div>
            </div>
        </div>
    </div>


    <div class="chat-input">
        <ChatInput @addMessage="(content) => pushToChat(content)"></ChatInput>
    </div>

</template>

<script>
import ChatInput from "@/ChatInput.vue";

export default {
    name: "MessagesWindow",
    components: {ChatInput},
    data() {
        return {
            messages: [
                {id: 0, text: ' Cześć, jak tam zajęcia z JS?', isMy: false, date: Date.now().toLocaleString().split(" ")[0]},
            ],
            isBotTyping:false,
        }
    },
    methods: {
        pushToChat(content){
            let lastId = this.messages[this.messages.length-1];
            this.messages.push({id: lastId+1, text: content, isMy: true, date:  Date.now()});
            this.botResponse(content);
        },

        async renderBotWriting(timeout=3000) {
            this.isBotTyping = true;
            await new Promise(resolve => setTimeout(resolve, timeout));
            this.isBotTyping = false;
        },

        async botToChat(content) {
            await this.renderBotWriting()
            let lastId = this.messages[this.messages.length-1];
            this.messages.push({id: lastId+1, text: content, isMy: false, date:  Date.now()});
        },

        async botWarning() {
            alert("Użytkownik proszony jest o zachowanie kultury");
            await this.renderBotWriting(1000)
            let lastId = this.messages[this.messages.length-1];
            this.messages.push(
                {id: lastId+1, text: "proszę, nie używaj takich słów", isMy: false, isWarning: true, date:  Date.now()});
        },

        containsWord(message, wordsList) {
            for(let index in wordsList){
                if(message.toLowerCase().includes(wordsList[index])) {
                    return true;
                }
            }
            return false;
        },

        botResponse(content){
            let bannedWords = ["chuj", "kurwa", "dupa", "dupy", "motyla noga", "cholera", "kurde"]
            if(this.containsWord(content, bannedWords)) {
                this.botWarning();
            }

            let howIsJSWordsGood = ["super", "świetnie", "wspaniale", "nieźle", "dobrze"]
            if(this.containsWord(content, howIsJSWordsGood)) {
                this.botToChat("Łał! Bardzo się cieszę. Nawet ja ostatnio polubiłem Vue.js");
            }

            let howIsJSWordsBad = ["kiepsko", "źle", "okropnie"]
            if(this.containsWord(content, howIsJSWordsBad)) {

                this.botToChat("Nie martw się. Odrobina treningu i będzie lepiej!");
            }

            let howIsJSWordsNeutral = ["tak sobie", "średnio", "nieciekawe", "nieciekawie", "ok"]
            if(this.containsWord(content, howIsJSWordsNeutral)) {

                this.botToChat("Może kolejne zajęcia bardziej Ci się spodobają");
            }

            let howYouDoinWords = ["jak leci", "co słychać", "co u ciebie", "co tam"]
            if(this.containsWord(content, howYouDoinWords)) {

                this.botToChat("Całkiem nieźle! Dzięki że pytasz :)");
            }

            let versionWords = ["/version"]
            if(this.containsWord(content, versionWords)) {

                this.botToChat("Wersja mojego softu to 0.1.8");
            }

            let weatherWords = ["/pogoda kraków"]
            if(this.containsWord(content, weatherWords)) {

                this.botToChat("Aktualnie w Krakowie jest 16 stopni");
            }
        }
    }
}
</script>

<style scoped>

.msg-box-line {
    width: 100%;
    margin-top: 8px;
    position: relative;
}

.msg-box-message-other {
    position: relative;
    display: inline-block;
    padding: 5px 20px;
    border-radius: 15px;
    cursor: default;
    background: #f1f1f1;
    transition: all 0.12s;
}

.msg-box-message-other-warning {
    color: red;
    font-weight: bold;
}

.msg-box-line-my{
    text-align: right;
}

.msg-box-message-my{
    position: relative;
    display: inline-block;
    padding: 5px 20px;
    border-radius: 15px;
    cursor: default;
    background: #3765ff;
    transition: all 0.12s;
    color: #fff;
}


.chat-input {
    width: 100%;
    position: relative;
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 10px;
}


.typing {
    align-items: center;
    display: flex;
    height: 17px;
}
.typing .dot {
    animation: mercuryTypingAnimation 1.8s infinite ease-in-out;
    border-radius: 50%;
    height: 7px;
    margin-right: 4px;
    vertical-align: middle;
    width: 7px;
    display: inline-block;
}
.typing .dot:nth-child(1) {
    animation-delay: 200ms;
}
.typing .dot:nth-child(2) {
    animation-delay: 300ms;
}
.typing .dot:nth-child(3) {
    animation-delay: 400ms;
}
.typing .dot:last-child {
    margin-right: 0;
}

@keyframes mercuryTypingAnimation {
    0% {
        transform: translateY(0px);
    }
    28% {
        transform: translateY(-7px);
    }
    44% {
        transform: translateY(0px);
    }
}


</style>