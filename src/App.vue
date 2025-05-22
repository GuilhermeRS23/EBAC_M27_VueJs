<script setup>
import { reactive } from 'vue';
import CampoValores from './components/CampoValores.vue';
import Header from './components/Header.vue';

const state = reactive({
  operador: "+",
  numeroA: 0,
  numeroB: 0,
});

const resultado = () => {
  const { operador } = state;
  const num1 = Number(state.numeroA);
  const num2 = Number(state.numeroB);

  if (operador === "-") {
    return num1 - num2;
  } else if (operador === "/") {
    return (num1 / num2).toFixed(2);
  } else if (operador === "*") {
    return num1 * num2;
  } else {
    return num1 + num2;
  }
};

</script>

<template>
  <div class="calculadora">
    <Header />
    <CampoValores :numero-a="state.numeroA" :alterar-valor-a="e => state.numeroA = e.target.value"
      :operador="e => state.operador = e.target.value" :numero-b="state.numeroB"
      :alterar-valor-b="e => state.numeroB = e.target.value" :resultado="resultado()" />
  </div>
</template>

<style scoped>
.calculadora {
  align-items: center;
  margin: auto;
  max-width: 720px;
}
</style>
