<script setup lang="ts">
import { ref, computed } from 'vue';
import type { Ref, ComputedRef } from 'vue';
import { RouterLink } from 'vue-router'
import router from '@/router';

const email: Ref<string> = ref('');
const password: Ref<string> = ref('');

const errors: Ref<Array<{ field: string; message: string }>> = ref([]);

const changeButtonState: ComputedRef<boolean> = computed(() => {
  return email.value.trim() !== '' && password.value.trim() !== '';
});

const submit = () => {
  clearErrors();
  if (email.value == 'kevcb2003@gmail.com' && password.value == '123456') {
    console.log('Inicio de sesión exitoso');
    router.push('/home');
  }
  if (email.value != 'kevcb2003@gmail.com') {
    errors.value.push({ field: 'email', message: 'El correo no ha sido registrado' });
  } else {
    if (password.value != '123456') {
      errors.value.push({ field: 'password', message: 'La contraseña no es la correcta' });
    }
  }
}

const clearErrors = () => {
  errors.value = [];
};
</script>

<template>
  <div class="container">
    <h1>Inicio de sesión</h1>
    <form class="form" @submit.prevent="submit()">
      <div class="form-inputs">
        <label for="email">Correo:</label>
        <input v-model="email" type="email" required />
        <span v-if="errors.some(error => error.field === 'email')" class="error">
          {{ errors.find(error => error.field === 'email')?.message }}
        </span>
      </div>
      <div class="form-inputs">
        <label for="password">Contraseña:</label>
        <input v-model="password" type="password" required />
        <span v-if="errors.some(error => error.field === 'password')" class="error">
          {{ errors.find(error => error.field === 'password')?.message }}
        </span>
      </div>
      <div>
        <button type="submit" :disabled="!changeButtonState">Ingresar</button>
      </div>
    </form>
    <p>¿No cuentas todavia con una cuenta?</p>
    <router-link to="/register" class="link">Regístrate aquí</router-link>
  </div>
</template>

<style scoped>
.container {
  width: fit-content;
  height: fit-content;
  text-align: center;
  margin: 0 .5rem;
  padding: 1rem;

  & h1 {
    font-size: 2rem;
    font-weight: bold;
    font-style: italic;
    margin-bottom: 1rem;
    color: #41B883;
  }

  & .form {
    width: 30vw;
    margin: 0 auto;
    padding: 20px;
    background-color: #34495E;
    border-radius: 8px;
    border: 2px solid #FFFFFF;
    box-shadow: 0 4px 8px rgb(255, 255, 255);

    & label {
      display: block;
      font-size: 1.6rem;
      font-weight: bold;
      color: #41B883;
    }

    & input {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      box-sizing: border-box;
      font-size: 1.1rem;
      border: 2px solid black;
      border-radius: 5px;
    }

    & button {
      background-color: #41B883;
      color: white;
      padding: 1rem;
      margin: 1rem;
      font-size: 1.6rem;
      font-weight: bold;
      border: 2px solid black;
      border-radius: 5px;
      cursor: pointer;
    }

    & button:disabled {
      background-color: #ccc;
      cursor: not-allowed;
    }

    & .error {
      color: white;
      font-size: 1.1rem;
      background-color: #3755da;
      padding: 5px;
      border: 2px solid black;
      border-radius: 5px;
      display: block;
      margin-top: 5px;
    }
  }

  & p {
    font-size: 1.5rem;
    margin-top: 1rem;
  }

  & .link {
    font-size: 1.5rem;
  }
}
</style>