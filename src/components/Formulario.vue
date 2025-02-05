<script setup>
    const props = defineProps(["cadastraTarefa", "tarefaTemporaria", "atualizaFiltro", "editaTarefaTemp"]);
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
      <div class="row">
        <div class="col">
          <input type="text" class="form-control" :value="props.tarefaTemporaria" @change="editaTarefaTemp" required>
        </div>

        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>

        <div class="col-md-2">
          <select class="form-control" @change="props.atualizaFiltro">
            <option value="todas">Todas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
</template>