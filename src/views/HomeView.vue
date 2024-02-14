<script setup lang="ts">
import UsersData from '@/data/UsersData';
import UsersList from '@/components/UsersList.vue';
</script>

<template>
  <div class="container">
    <h1>Lista de Usuarios</h1>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Nombre(s)</th>
          <th>Apellidos</th>
          <th>Edad</th>
          <th>Correo</th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        <UsersList v-bind="users" v-for="(users, index) in UsersData" :key="index" />
      </tbody>
    </table>
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
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 1rem;
  border-radius: 15px;
}

th {
  border: 1px solid white;
  padding: 1rem;
  color: #41B883;
  font-size: 1.5rem;
  font-weight: bold;
  text-align: left;
  background-color: #34495E;
}
</style>