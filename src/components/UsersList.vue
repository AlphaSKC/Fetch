<script setup lang="ts">
import type { IUser } from '@/interfaces/IUser';
const props = defineProps<IUser>();
</script>

<template>
    <tr>
        <td>{{ props.id + 1 }}</td>
        <td>{{ props.name }}</td>
        <td>{{ props.lastname }}</td>
        <td>{{ props.age }}</td>
        <td>{{ props.email }}</td>
        <td>
            <button class="edit">Editar</button>
            <button class="delete">Eliminar</button>
        </td>
    </tr>
</template>

<style scoped>
td {
    border: 1px solid white;
    padding: 8px;
    color: white;
    font-size: 1.1rem;
    text-align: left;

    & button {
        padding: 1rem;
        font-size: 1.1rem;
        font-weight: bold;
        color: white;
        margin: 0.5rem;
        border-radius: 15px;
    }

    & .edit {
        background-color: #41B883;
    }

    & .delete {
        background-color: #E74C3C;
    }
}
</style>