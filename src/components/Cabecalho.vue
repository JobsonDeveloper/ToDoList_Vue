<script setup>
    const props = defineProps(["tarefasPendentes"]);
</script>

<template>
    <header class="p-5 mb-4 rounded-3 text-center">
        <h1>To Do List</h1>
        <p>
            Você possui {{ props.tarefasPendentes }} tarefas pendentes
        </p>
    </header>
</template>

<style scoped>
    header {
        background-color: #0078bd;
    }

    h1, p {
        color: #fff;
    }
</style>