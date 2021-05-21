<template>
  <div>
    <!--    <input v-model="state">-->
    <!--    <button @click="setState">Задать состояние</button>-->
    <!--    <button @click="getData">Получить состояние</button>-->
    <!--    {{ result }}-->
    <!--    <label>-->
    <!--      Адрес сервера:-->
    <!--      <input v-model="baseUrl">-->
    <!--    </label>-->
    <div>
      <label>
        Автор
        <input v-model="author">
      </label>
      <label>
        Сообщение
        <input v-model="message">
      </label>
      <button @click="sendMessage">Отправить</button>
    </div>
    <div v-for="message in chat.messages">
      {{ message }}
    </div>
  </div>
</template>

<script>
import {defineComponent} from 'vue';
import axios from 'axios';

export default defineComponent({
  data() {
    return {
      author: '',
      message: '',
      result: {},
      state: 0,
      count: 0,
      baseUrl: 'http://10.10.58.125:8080/',
      chat: {},
    }
  },
  created() {
    this.getChat();
  },
  methods: {
    sendMessage() {
      axios.post(this.baseUrl + 'message',
          {
            author: this.author,
            message: this.message
          }
      ).then(res => console.log(res));
    },
    getChat() {
      axios.get(this.baseUrl + 'chat').then(res => this.chat = res.data);
    },
    incrementCounter() {
      this.count++;
    },
    getData() {
      axios.get(this.baseUrl + 'state').then(res => this.result = res.data);
    },
    setState() {
      axios
          .post(this.baseUrl + 'state', {state: this.state})
          .then(res => console.log(res));
    }
  }
})

</script>

<style scoped>
a {
  color: #42b983;
}
</style>
