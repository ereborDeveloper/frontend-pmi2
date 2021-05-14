<template>
  <div>
    <!--    <input v-model="state">-->
    <!--    <button @click="setState">Задать состояние</button>-->
    <!--    <button @click="getData">Получить состояние</button>-->
    <!--    {{ result }}-->
    <label>
      Адрес сервера:
      <input v-model="baseUrl">
    </label>
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
