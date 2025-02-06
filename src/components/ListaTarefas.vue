<script setup>
    const props = defineProps(["tarefas","remover", "editarTarefa"]);
</script>

<template>
    <ul class="list-group mt-4" v-for="tarefas in props.tarefas">
        <li class="list-group-item d-flex justify-content-between">
            <div>
                <input :checked="tarefas.finalizada" :id="tarefas.titulo" type="checkbox"
                    @change="editarTarefa(tarefas.titulo, tarefas.finalizada)">
                <label :for="tarefas.titulo" class="ms-3" :class="{ done: tarefas.finalizada }">
                    {{ tarefas.titulo }}
                </label>
            </div>
            <i class="bi bi-x-circle-fill list__icon" @click="remover(tarefas.titulo)"></i>
        </li>
    </ul>
</template>

<style scoped>
.done {
  text-decoration: line-through;
  color: #d0cfcfcd;
}

li {
    background-color: #001d4b;
    border: 1px solid #ffffff4e;
    box-shadow: 3px 3px 1px #fff;
}

label {
    color: #fff;
    cursor: pointer;
    text-transform: capitalize;
}

.list__icon {
    color: #f00;
    cursor: pointer;
}
</style>
