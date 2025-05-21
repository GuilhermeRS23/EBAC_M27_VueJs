<script setup>
const props = defineProps(["tarefas"]);
</script>
<template>
    <div v-if="props.tarefas.length === 0" class="alert alert-primary mt-2" role="alert">
        <span>Nenhuma tarefa encontrada</span>
    </div>
    <ul v-else class="list-group mt-4">.
        <li class="list-group-item" v-for="tarefa in props.tarefas">
            <input @change="e => tarefa.finalizada = e.target.checked" :checked="tarefa.finalizada"
                :id="tarefa.descricao" type="checkbox">
            <label :for="tarefa.descricao" class="ms-3" :class="{ done: tarefa.finalizada }">
                {{ tarefa.descricao }}
            </label>
        </li>
    </ul>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>
