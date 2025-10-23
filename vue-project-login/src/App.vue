<script setup>
  import { reactive, provide, ref, watch } from 'vue';
  import LoginForm from './components/LoginForm.vue';
  import UserInfo from './components/UserInfo.vue';

  // Funcion sobre el estado del usuario
  const userState = reactive({
    isLoggedIn: false,
    username: ''
  });

  function login(username, password) {
    if (username === 'admin' && password === '1234') {
      userState.isLoggedIn = true;
      userState.username = username;
    } else {
      alert('Usuario o contraseña incorrectos');
    }
  };

  function logout() {
    userState.isLoggedIn = false;
    userState.username = '';
  };

  // Proveer datos a los forms hijos
  provide('userState', userState);
  provide('logout', logout);

  // Watcher  observar cambios en el login
  watch(
    () => userState.isLoggedIn,
    (nuevoValor) => {
      alert(nuevoValor ? 'Sesión iniciada' : 'Sesión cerrada');
    }
  );



</script>

<template>
    <fieldset class="app">
      
    <LoginForm 
      v-if="!userState.isLoggedIn" 
      @login="login" 
    />
    <UserInfo v-else />
    </fieldset>

</template>

<style scoped>
.app {
  max-width: 400px;
  margin: 2rem auto;
  text-align: center;
  background: #262626;
  padding: 1.5rem;
  border-radius: 12px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}
</style>
