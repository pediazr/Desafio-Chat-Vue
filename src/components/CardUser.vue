<script setup>
import { ref } from 'vue';
const props = defineProps({
    user: {
        type: Object,
        required: true,
    },
});
const emit = defineEmits(['sendMsg']);
const mensaje = ref('');
const color = ref('');
const enviarMensaje = () => {
    emit('sendMsg', mensaje.value, color.value, props.user.name.first, props.user.side);
    mensaje.value = '';
}
</script>
<template>
    <div class="user-component">

        <div class="card">
            <img :src="user.picture.large" class="card-img-top" alt="foto usuario" />
            <div class="card-body">
                <h5 class="card-title">{{ user.name.first }} {{ user.name.last }}</h5>
                <form @submit.prevent="enviarMensaje">
                    <input v-model="color" type="color" class="col-12 rounded" />
                    <textarea v-model="mensaje" class="col-12 form-control mb-1" cols="5" required></textarea>
                    <button class="btn btn-success col-12">Enviar</button>
                </form>
            </div>
        </div>
    </div>
</template>