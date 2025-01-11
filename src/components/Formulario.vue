<script setup>
const props = defineProps(['cadastrarTarefa', 'tarefaTemp', 'editarTarefa', 'mudarFiltro'])
</script>

<template>
  <form @submit.prevent="props.cadastrarTarefa">
    <div class="row">
      <div class="col">
        <input :value="props.tarefaTemp" @change="props.editarTarefa" class="form-control" type="text"
          placeholder="Digite aqui sua tarefa" required>
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="props.mudarFiltro" class="form-control">
          <option value="todas">Todas</option>
          <option value="feitas">Feitas</option>
          <option value="pendentes">Pendentes</option>
        </select>
      </div>
    </div>
  </form>
</template>