<script setup>

import "bootstrap/dist/css/bootstrap.min.css";
import { reactive } from "vue";

const estado = reactive({
  tarefas: [
    {
      titulo: "Estudar TypeScript",
      finalizada: false,
    },
    {
      titulo: "Estudar Sass",
      finalizada: true,
    },
    {
      titulo: "Estudar React.ts",
      finalizada: false,
    },
    {
      titulo: "Estudar Spring Boot",
      finalizada: true,
    }
  ],
  filtro: "todas",
  tarefaTemporaria: "",
});

function atualizaFiltro(e) {
  estado.filtro = e.target.value;
}

// function toggleChecked(e) {
//   tarefas.finalizada = e.target.checked;
// }

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefas => !tarefas.finalizada);
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefas => tarefas.finalizada);
}

const getTarefas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case "pendentes":
      return getTarefasPendentes();
      break;
    case "finalizadas":
      return getTarefasFinalizadas();
      break;
    default:
      return estado.tarefas;
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemporaria,
    finalizada: false
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemporaria = "";
}

</script>

<template>
  <main class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>

    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input type="text" class="form-control" :value="estado.tarefaTemporaria" @change="event => estado.tarefaTemporaria = event.target.value" required>
        </div>

        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>

        <div class="col-md-2">
          <select class="form-control" @change="atualizaFiltro">
            <option value="todas">Todas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>

    <ul class="list-group mt-4" v-for="tarefas in getTarefas()">
      <li class="list-group-item">
        <input :checked="tarefas.finalizada" :id="tarefas.titulo" type="checkbox" @change="event => tarefas.finalizada = event.target.checked">
        <label :for="tarefas.titulo" class="ms-3" :class="{ done: tarefas.finalizada }">
          {{ tarefas.titulo }}
        </label>
      </li>
    </ul>
  </main>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
