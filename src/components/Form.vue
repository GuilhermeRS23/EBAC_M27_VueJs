<script setup>
const props = defineProps(["adicionarTarefa", "tarefaTemp", "alterarTarefa", "filtro", "alterarTemp"])
</script>

<template>
    <form @submit.prevent="props.adicionarTarefa">
        <div class="row">
            <div class="col">
                <input class="form-control" type="text" placeholder="Digite uma tarefa..." :value="props.tarefaTemp"
                    @change="props.alterarTemp" required>
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Adicionar</button>
            </div>
            <div class="col-md-2">
                <select class="form-control" @change="props.filtro">
                    <option value="todas">Todas as tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>

<!-- e => estado.tarefaTemp = e.target.value : alterarTarefa -->
<!-- e => estado.filtro = e.target.value : filtro -->
