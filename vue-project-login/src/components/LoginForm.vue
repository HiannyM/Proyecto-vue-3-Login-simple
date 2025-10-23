<script setup>
    import { ref, computed, watch } from 'vue';

    //Props iniciar sesión
    const props = defineProps({
    title: {
        type: String,
        default: 'Iniciar sesión'
    }
    });

    // Emitir evento al padre
    const emit = defineEmits(['login']);

    // Datos del formulario
    const username = ref('');
    const password = ref('');

    const formValid = computed(() => username.value && password.value);

    // Watcher para limpiar cambios en el nombre
    watch(username, (nuevo) => {
        console.log('Usuario digitado:', nuevo)
    });

    // Función de login
    function handleSubmit() {
    if (!formValid.value) {
        alert('Por favor complete todos los campos.');
        return;
    }
    emit('login', username.value, password.value)
        username.value = '';
        password.value = '';
    };

</script>

<template>
    <div class="card">
        <h2>✨ {{ title }}</h2>
        <input 
            v-model="username" 
            type="text" 
            placeholder="Usuario" 
        />
        <input 
            v-model="password" 
            type="password" 
            placeholder="Contraseña" 
        />
        <button @click="handleSubmit"> Entrar</button>
    </div>

    </template>

    <style scoped>
    .card {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    }
    input {
    padding: 0.5rem;
    border-radius: 8px;
    border: none;
    border-top: 2px solid #0056b3; 

    }
    button {
    background: #007bff;
    color: white;
    padding: 0.5rem;
    border-radius: 8px;
    border: none;
    cursor: pointer;
    }
    button:hover {
    background: #0056b3;
    }
</style>
