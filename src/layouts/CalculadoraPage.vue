<template>
  <div class="center-container">
    <div class="container">
      <div class="display">{{ display || 0 }}</div>

      <div @click="clear" class="del operacao">DEL</div>
      <div @click="metodoDivide" class="operacao">/</div>
      <div @click="getDigitado('7')" class="numeros">7</div>
      <div @click="getDigitado('8')" class="numeros">8</div>
      <div @click="getDigitado('9')" class="numeros">9</div>

      <div @click="metodoMultiplicar" class="operacao">*</div>
      <div @click="getDigitado('4')" class="numeros">4</div>
      <div @click="getDigitado('5')" class="numeros">5</div>
      <div @click="getDigitado('6')" class="numeros">6</div>

      <div @click="metodoSubtrair" class="operacao">-</div>
      <div @click="getDigitado('1')" class="numeros">1</div>
      <div @click="getDigitado('2')" class="numeros">2</div>
      <div @click="getDigitado('3')" class="numeros">3</div>

      <div @click="metodoSomar" class="operacao">+</div>
      <div @click="getDigitado('0')" class="zero numeros">0</div>
      <div @click="ponto" class="numeros">.</div>
      <div @click="metodoCalcularOperacao" class="operacao">=</div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
//variáveis
const display = ref("");
const operadorClicado = ref(false);
const operador = ref(null);
const resultadoClick = ref(null);

// metodos
const clear = () => {
  display.value = "";
  operador.value = null;
  resultadoClick.value = null;
};

const getDigitado = (digit) => {
  if (operadorClicado.value) {
    display.value = "";
    operadorClicado.value = false;
  }
  display.value += digit;
};

const metodoSomar = () => {
  operador.value = (a, b) => a + b;
  resultadoClick.value = display.value;
  operadorClicado.value = true;
};

const metodoDivide = () => {
  operador.value = (a, b) => a / b;
  resultadoClick.value = display.value;
  operadorClicado.value = true;
};

const metodoSubtrair = () => {
  operador.value = (a, b) => a - b;
  resultadoClick.value = display.value;
  operadorClicado.value = true;
};

const metodoMultiplicar = () => {
  operador.value = (a, b) => a * b;
  resultadoClick.value = display.value;
  operadorClicado.value = true;
};

const ponto = () => {
  if (display.value.indexOf(".") === -1) {
    display.value += ".";
  }
};

const metodoCalcularOperacao = () => {
  if (resultadoClick.value !== null && display.value !== "") {
    display.value = `${operador.value(
      parseFloat(resultadoClick.value),
      parseFloat(display.value)
    )}`;
    resultadoClick.value = null;
  }
};
</script>

<style scoped>
html,
body {
  background-color: black;
}
.center-container {
  display: flex;
  justify-content: center;
  align-items: center;
}
.container {
  font-weight: bold;
  color: white;
  display: grid;
  grid-template-rows: repeat(6, 0.5fr);
  grid-template-columns: repeat(4, 1fr);
  width: 300px;
  height: 400px;
}

.zero {
  grid-column: 1/3;
}

.del {
  grid-column: 1/4;
}

.display {
  padding: 30px;
  border: 1px solid;
  font-size: 2rem;
  grid-column: 1/5;
  text-align: right;
  color: white;
  background-color: #1c1c1c;
}

.operacao,
.numeros {
  padding: 30px;
  font-size: 1.5rem;
  border: 1px solid;
  text-align: center;
  transition: background-color 1s;
}

.operacao {
  background-color: #df2d2dff;
}

.numeros {
  background-color: #313127ff;
}

.operacao:active,
.numeros:active {
  background-color: rgb(151, 14, 14);
}
</style>
