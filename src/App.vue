<script setup>
import { reactive } from "vue";

const estado = reactive({
  filtro: "todos",
  tarefaTemp: "",
  tarefas: [
    {
      descricao: "Estudar Vue.js",
      finalizada: false
    },
    {
      descricao: "Estudar React.Js",
      finalizada: true
    },
    {
      descricao: "Realizar uma caminhada",
      finalizada: false
    }
  ]
});

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada);
};
const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada);
};

const getFiltroTarefas = () => {
  const { filtro } = estado;
  if (filtro === "finalizadas") {
    return getTarefasFinalizadas();
  } else if (filtro === "pendentes") {
    return getTarefasPendentes();
  } else {
    return estado.tarefas
  }
}

const adicionarTarefa = () => {
  const novaTarefa = {
    descricao: estado.tarefaTemp,
    finalizada: false,
  }
  estado.tarefas.push(novaTarefa);
  estado.tarefaTemp = "";
}
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 bg-light rounded-3">
      <h1>Lista de Tarefas</h1>
      <p>Você possui {{ getTarefasPendentes().length }} tarefas pendentes.</p>
    </header>
    <form @submit.prevent="adicionarTarefa">
      <div class="row">
        <div class="col">
          <input class="form-control" type="text" placeholder="Digite uma tarefa..." :value="estado.tarefaTemp"
            @change="e => estado.tarefaTemp = e.target.value" required>
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Adicionar</button>
        </div>
        <div class="col-md-2">
          <select class="form-control" @change="e => estado.filtro = e.target.value">
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>

    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getFiltroTarefas()">
        <input @change="e => tarefa.finalizada = e.target.checked" :checked="tarefa.finalizada" :id="tarefa.descricao"
          type="checkbox">
        <label :for="tarefa.descricao" class="ms-3" :class="{ done: tarefa.finalizada }">
          {{ tarefa.descricao }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
