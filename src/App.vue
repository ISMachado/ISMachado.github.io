<template>
  <div id="app">
    <login-form v-if="isLoginFormVisible" @toggleForm="toggleForm"/>
    <register-form v-else @toggleForm="toggleForm"/>
  </div>
</template>

<script>
import LoginForm from './components/LoginForm.vue';
import RegisterForm from './components/RegisterForm.vue';

export default {
  components: {
    LoginForm,
    RegisterForm
  },
  data() {
    return {
      isLoginFormVisible: true
    };
  },
  methods: {
    toggleForm() {
      this.isLoginFormVisible = !this.isLoginFormVisible;
    }
  }
};
</script>

<style>
/* Estilização global */
body {
  font-family: Arial, sans-serif;
  background-color: #f5f5f5;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
#app {
  width: 100%;
  max-width: 400px;
}
</style>
