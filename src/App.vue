<template>

    <div class="chat">
    <ChatWindow></ChatWindow>
    </div>
</template>

<script>
import ChatWindow from './ChatWindow.vue'

export default {
  name: 'App',
  components: {
      ChatWindow
  }
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  font-family: 'Roboto';

}

.chat{
    display: block;
    position: relative;
    max-width: 400px;
    margin: 70px auto;
    padding: 10px;
    background: #fff;
    border-radius: 15px;
    box-shadow: 0 0 30px #eee;
    font-size: 17px;
}



</style>
