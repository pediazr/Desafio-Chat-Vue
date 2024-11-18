<script setup>
const props = defineProps({
    mensajes: {
        type: Array,
        required: true,
    },
});
</script>
<template>
    <div class="chatbox rounded shadow-lg">
        <h2 class="text-center">ChatBox</h2>
        <hr>
        <div v-for="(mensaje, id) in mensajes" :key="id" :class="mensaje.side == 'left' ? 'text-start' : 'text-end'">
            <span>{{ mensaje.name }}</span>
            <p class="colorLine rounded mx-2 fw-medium" :style="{ backgroundColor: mensaje.color }">
                {{ mensaje.mensaje }}
            </p>
        </div>
    </div>
</template>
<style scoped>
.colorLine {
    padding: 10px;
    margin: 5px;
}

.chatbox {
    background-color: #d2d2c6;
}
</style>