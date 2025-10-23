<script setup>
    import { inject, computed } from 'vue';

    // Inyectar el estado del usuario y el método de logout
    const userState = inject('userState');
    const logout = inject('logout');

    // Mensaje si el usuario ha iniciado sesión
    const welcomeMsg = computed(() => `Bienvenido, ${userState.username}!`);
</script>

<template>
    <transition name="fade">
        <div class="card">
        <h2>{{ welcomeMsg }}</h2>
        <p>Has iniciado sesión correctamente 👍</p>
        <button @click="logout">Cerrar sesión</button>
        </div>
    </transition>
</template>

<style scoped>
    .card {
        background: #44403B;
        padding: 1rem;
        border-radius: 10px;
        box-shadow: 0 3px 6px rgba(0, 0, 0, 0.1);
    }
    button {
        background: #dc3545;
        color: white;
        border: none;
        padding: 0.4rem 1rem;
        border-radius: 8px;
        cursor: pointer;
        }
    button:hover {
        background: #b02a37;
    }
    .fade-enter-active,
    .fade-leave-active {
        transition: opacity 0.5s;
    }
    .fade-enter-from,
    .fade-leave-to {
        opacity: 0;
    }
</style>
