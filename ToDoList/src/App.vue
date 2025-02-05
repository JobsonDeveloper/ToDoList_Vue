<script setup>

import "bootstrap/dist/css/bootstrap.min.css";
import { reactive } from "vue";
import Cabecalho from "./components/Cabecalho.vue";
import Formulario from "./components/Formulario.vue";
import ListaTarefas from "./components/ListaTarefas.vue";

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
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>

    <Formulario :cadastra-tarefa="cadastraTarefa" :tarefa-temporaria="tarefaTemporaria" :atualiza-filtro="atualizaFiltro" :edita-tarefa-temp="event => estado.tarefaTemporaria = event.target.value"/>

    <ListaTarefas :tarefas="getTarefas()"/>
  </main>
</template>
