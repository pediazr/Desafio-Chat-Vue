<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import ChatBox from './components/ChatBox.vue';
import CardUser from './components/CardUser.vue';

const userLeft = ref({});
const userRight = ref({});
const mensajes = ref([]);

const getUsuarios = async () => {
  try {
    const url = "https://randomuser.me/api?results=2";
    const { data } = await axios.get(url);
    userLeft.value = { ...data.results[0], side: 'left' };
    userRight.value = { ...data.results[1], side: 'right' };
  } catch (error) {
    console.log(error)
  }
}

const enviarMensaje = (mensaje, color, name, side) => {
  mensajes.value.push({ mensaje, color, name, side });
}

onMounted(getUsuarios());

</script>
<template>
  <div id="App">
    <h1>Chat Vue 💬</h1>
    <br>
    <div class="container">
      <div class="row">
        <CardUser :user="userLeft" @sendMsg="enviarMensaje" class="col-4" v-if="Object.keys(userLeft).length > 0" />
        <ChatBox :mensajes="mensajes" class="col-4" />
        <CardUser :user="userRight" @sendMsg="enviarMensaje" class="col-4" v-if="Object.keys(userRight).length > 0" />
      </div>
    </div>

  </div>
</template>
