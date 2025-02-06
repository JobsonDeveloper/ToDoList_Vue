<script setup>

import "bootstrap/dist/css/bootstrap.min.css";
import { reactive } from "vue";
import Cabecalho from "./components/Cabecalho.vue";
import Formulario from "./components/Formulario.vue";
import ListaTarefas from "./components/ListaTarefas.vue";

const estado = reactive({
  tarefas: [
  ],
  remover: "",
  filtro: "todas",
  tarefaTemporaria: "",
});

function atualizaFiltro(e) {
  estado.filtro = e.target.value;
}

const removeItem = (item) => {
  estado.tarefas.forEach((elemento) => {
    if (elemento.titulo === item) {
      const index = estado.tarefas.indexOf(elemento);
      estado.tarefas.splice(index, 1);
    }
  })
}

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

const atualizaLocalStorage = () => {

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
  <main class="page">
    <section class="container">
      <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
      <Formulario :cadastra-tarefa="cadastraTarefa" :tarefa-temporaria="tarefaTemporaria"
        :atualiza-filtro="atualizaFiltro" :edita-tarefa-temp="event => estado.tarefaTemporaria = event.target.value" />
      <ListaTarefas :tarefas="getTarefas()" :remover="removeItem" />
    </section>
  </main>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.page {
  display: flex;
  justify-content: center;
  padding: 20px 0 0;
  min-height: 100vh;
  background-color: #000f27;
  margin: 0 auto;
}

@media (max-width: 576px) {
  .page {
    padding: 20px 1rem;
  }
}
</style>