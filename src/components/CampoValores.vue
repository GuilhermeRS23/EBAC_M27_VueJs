<script setup>
const props = defineProps(["resultado", "operador", "numeroA", "numeroB", "alterarValorA", "alterarValorB"]);
</script>

<template>
    <div class="row g-3 p-5 mb-4 bg-light rounded-3 text-center">
        <div class="col-3">
            <input type="number" class="form-control text-center" :value="props.numeroA" @keyup="props.alterarValorA">
        </div>
        <div class="col-2">
            <select class="form-control text-center" @change="props.operador">
                <option value="+">+</option>
                <option value="-">-</option>
                <option value="/">:</option>
                <option value="*">x</option>
            </select>
        </div>
        <div class="col-3">
            <input type="number" class="form-control text-center" :value="props.numeroB" @keyup="props.alterarValorB">
        </div>
        <div class="col-1">
            <input readonly class="text-center form-control" value="=">
        </div>
        <div class="col-3">
            <input readonly class="form-control text-center p-2" :value="props.resultado">
        </div>
    </div>
</template>