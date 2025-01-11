<script setup>
const props = defineProps(['tarefasFiltradas'])
</script>
<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefasFiltradas">
            <input @change="event => tarefa.finalizada = event.target.checked" :checked="tarefa.finalizada"
                :id="tarefa.titulo" type="checkbox">
            <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</template>
<style scoped>
.done {
    text-decoration: line-through;
}
</style>