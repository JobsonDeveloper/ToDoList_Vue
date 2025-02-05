<script setup>
    const props = defineProps(["tarefas"]);
</script>

<template>
    <ul class="list-group mt-4" v-for="tarefas in props.tarefas">
        <li class="list-group-item">
            <input :checked="tarefas.finalizada" :id="tarefas.titulo" type="checkbox"
                @change="event => tarefas.finalizada = event.target.checked">
            <label :for="tarefas.titulo" class="ms-3" :class="{ done: tarefas.finalizada }">
                {{ tarefas.titulo }}
            </label>
        </li>
    </ul>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
