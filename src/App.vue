<script setup>
import Header from "./components/Header.vue";
import Form from "./components/Form.vue";
import ListTask from "./components/ListTask.vue";
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
    <Header :tarefas-pendentes="getTarefasPendentes().length" />
    <Form :adicionar-tarefa="adicionarTarefa" :tarefa-temp="estado.tarefaTemp"
      :alterar-temp="e => estado.tarefaTemp = e.target.value" :alterar-tarefa="e => estado.tarefaTemp = e.target.value"
      :filtro="e => estado.filtro = e.target.value" />
    <ListTask :tarefas="getFiltroTarefas()" />
  </div>
</template>
