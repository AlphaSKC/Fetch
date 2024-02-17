<script setup lang="ts">
import { ref, onMounted, computed } from 'vue';
import type { Ref, ComputedRef } from 'vue';

const name: Ref<string> = ref('');
const lastname: Ref<string> = ref('');
const age: Ref<number> = ref(0);
const email: Ref<string> = ref('');
const password: Ref<string> = ref('');
const errors: Ref<Array<{ field: string; message: string }>> = ref([]);

const changeButtonState: ComputedRef<boolean> = computed(() => {
  return errors.value.length === 0;
});

const validateForm = () => {
  clearErrors();

  if (name.value.trim() === '') {
    errors.value.push({ field: 'name', message: 'El nombre es obligatorio y no puede quedarse vacio' });
  }
  if (lastname.value.trim() === '') {
    errors.value.push({ field: 'lastname', message: 'El apellido es obligatorio y no puede quedarse vacio' });
  }
  if (lastname.value == name.value) {
    errors.value.push({ field: 'lastname', message: 'El apellido no puede ser igual al nombre' });
  }
  if (age.value < 18) {
    errors.value.push({ field: 'age', message: 'Debes ser mayor de edad para registrarte' });
  }
  if (email.value.trim() === '') {
    errors.value.push({ field: 'email', message: 'El correo es obligatorio y no puede quedarse vacio' });
  }
  if (password.value.trim() === '') {
    errors.value.push({ field: 'password', message: 'La contraseña es obligatoria y no puede quedarse vacia' });
  }
  if (password.value.length < 6) {
    errors.value.push({ field: 'password', message: 'La contraseña debe tener al menos 6 caracteres' });
  }
};

const clearErrors = () => {
  errors.value = [];
};

onMounted(() => {
  validateForm();
});

</script>

<template>
  <div class="container">
    <h1>Registro de cuenta</h1>
    <form class="form">
      <div class="form-inputs">
        <label for="name">Nombre(s):</label>
        <input @input="validateForm()" v-model="name" type="text" placeholder="Ingresa tu(s) nombre(s)" />
        <span v-if="errors.some(error => error.field === 'name')" class="error">
          {{ errors.find(error => error.field === 'name')?.message }}
        </span>
      </div>
      <div class="form-inputs">
        <label for="lastname">Apellidos:</label>
        <input @input="validateForm()" v-model="lastname" type="text" placeholder="Ingresa tus apellidos" />
        <span v-if="errors.some(error => error.field === 'lastname')" class="error">
          {{ errors.find(error => error.field === 'lastname')?.message }}
        </span>
      </div>
      <div class="form-inputs">
        <label for="age">Edad:</label>
        <input @input="validateForm()" v-model="age" type="number" placeholder="Ingresa tu edad" />
        <span v-if="errors.some(error => error.field === 'age')" class="error">
          {{ errors.find(error => error.field === 'age')?.message }}
        </span>
      </div>
      <div class="form-inputs">
        <label for="email">Correo:</label>
        <input @input="validateForm()" v-model="email" type="email" placeholder="Ingresa tu correo electrónico" />
        <span v-if="errors.some(error => error.field === 'email')" class="error">
          {{ errors.find(error => error.field === 'email')?.message }}
        </span>
      </div>
      <div class="form-inputs">
        <label for="password">Contraseña:</label>
        <input @input="validateForm()" v-model="password" type="password" placeholder="Ingresa tu contraseña" />
        <span v-if="errors.some(error => error.field === 'password')" class="error">
          {{ errors.find(error => error.field === 'password')?.message }}
        </span>
      </div>
      <div>
        <button type="submit" :disabled="!changeButtonState">Registrar</button>
      </div>
    </form>
    <p>¿Ya tienes una cuenta?</p>
    <router-link to="/" class="link">Inicia sesión aquí</router-link>
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
      margin-top: 1rem;
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