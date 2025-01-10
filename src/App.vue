<script setup>
import { reactive } from "vue";

const estado = reactive({
  tarefaTemp: '',
  filtro: 'todas',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizada: false
    },
    {
      titulo: 'Estudar SASS',
      finalizada: false,
    },
    {
      titulo: 'Ir pra a academia',
      finalizada: true
    }
  ]
})

const getTarefasPedentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}
const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas = () => {
  const { filtro } = estado;
  switch (filtro) {
    case 'pendentes':
      return getTarefasPedentes();
      break;
    case 'feitas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
      break;
  }

}
const cadastrarTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';
}
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>Você possui {{ getTarefasPedentes().length }} tarefas pedentes</p>
    </header>
    <form @submit.prevent="cadastrarTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @change="event => estado.tarefaTemp = event.target.value"
            class="form-control" type="text" placeholder="Digite aqui sua tarefa" required>
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="event => estado.filtro = event.target.value" class="form-control">
            <option value="todas">Todas</option>
            <option value="feitas">Feitas</option>
            <option value="pendentes">Pendentes</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="event => tarefa.finalizada = event.target.checked" :checked="tarefa.finalizada"
          :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>

</template>
<style scoped>
.done {
  text-decoration: line-through;
}
</style>
