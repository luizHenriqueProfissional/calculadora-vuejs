<script setup>
    import { reactive } from 'vue';

const estado = reactive({
    n1: '',
    n2: '',
    operacoes: {
        soma: (a, b) => a + b,
        subtracao: (a, b) => a - b,
        multiplicacao: (a, b) => a * b,
        divisao: (a, b) => (b !== 0 ? a / b : 'Divisao por zero'),
    },
    resultado: 0,
});

const calculaResultado = () => {
    const { n1, n2, operacaoMatematica } = estado;
    const num1 = parseFloat(n1);
    const num2 = parseFloat(n2);
    estado.resultado = !isNaN(num1) && !isNaN(num2) ? estado.operacoes[operacaoMatematica](num1, num2) : '';
};
</script>

<template>
  <h1 class="mt-5 mb-5">Calculadora</h1>
  <div class="container d-flex">
    <input class="form-control m-1" v-model="estado.n1" type="number" @input="calculaResultado">
        <select  class="form-control m-1" v-model="estado.operacaoMatematica" @change="calculaResultado">
            <option value="soma">+</option>
            <option value="subtracao">-</option>
            <option value="multiplicacao">x</option>
            <option value="divisao">/</option>
        </select>
        <input type="number" class="form-control m-1 " v-model="estado.n2" @input="calculaResultado">
  </div>
  <div class="container d-flex mt-2">
    <p class="form-control m-1">Seu resultado será:</p>
    <p class="form-control m-1 bg-primary color">{{ estado.resultado }}</p>
  </div> 
</template>

<style scoped>
 h1{
    text-align: center;
  }
  input{
    text-align: center;
  }
  p{
    text-align: center;
  }
  select{
    text-align: center;
  }
  .color{
    color: #fff;
  }

</style>