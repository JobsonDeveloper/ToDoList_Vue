<script setup>
const props = defineProps(["cadastraTarefa", "tarefaTemporaria", "atualizaFiltro", "editaTarefaTemp"]);
</script>

<template>
  <form @submit.prevent="props.cadastraTarefa">
    <div class="row">
      <div class="col-12 col-md-8">
        <input type="text" class="form-control" placeholder="Nome da tarefa" :value="props.tarefaTemporaria" @change="editaTarefaTemp" required>
      </div>

      <div class="mt-3 mt-md-0 col-md-2 col-sm-6">
        <button type="submit" class="btn form__button">Cadastrar</button>
      </div>

      <div class="mt-3 mt-md-0 col-md-2 col-sm-6">
        <select class="form-control" @change="props.atualizaFiltro">
          <option value="todas">Todas</option>
          <option value="pendentes">Pendentes</option>
          <option value="finalizadas">Finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>

<style scoped>
.form__button {
  width: 100%;
  background-color: #0078bd;
  color: #ffffff;
}

input, select {
  background-color: #3c4960;
  border-color: #3c4960;
  color: #fff;
}


input::placeholder {
  color: #cbcbcb;
}

@media (min-width: 768px) {
  form {
    .form__button {
      width: max-content;
    }
  }
}
</style>