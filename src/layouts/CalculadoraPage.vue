<template>
  <q-layout view="lHh Lpr lFf">
    <q-page-container>
      <q-page class="flex flex-center bg-black text-white">
        <q-card flat bordered class="q-pa-md" style="width: 320px">
          <!-- Display -->
          <q-input
            v-model="display"
            readonly
            dense
            class="q-pa-sm text-end text-h5 bg-grey-9 text-white"
            style="border: 1px solid #1c1c1c; color: white"
          />

          <!-- Botões -->
          <div class="q-gutter-sm q-pt-md">
            <!-- Primeira linha (DEL, /) -->
            <div class="row q-gutter-sm">
              <q-btn
                @click="clear"
                label="DEL"
                color="negative"
                flat
                unelevated
                class="col"
              />
              <q-btn
                @click="metodoDivide"
                label="/"
                color="primary"
                flat
                unelevated
                class="col"
              />
            </div>

            <!-- Linha com números e operadores -->
            <div class="row q-gutter-sm">
              <q-btn
                @click="getDigitado('7')"
                label="7"
                flat
                unelevated
                class="col bg-grey-7"
              />
              <q-btn
                @click="getDigitado('8')"
                label="8"
                flat
                unelevated
                class="col bg-grey-7"
              />
              <q-btn
                @click="getDigitado('9')"
                label="9"
                flat
                unelevated
                class="col bg-grey-7"
              />
              <q-btn
                @click="metodoMultiplicar"
                label="*"
                color="primary"
                flat
                unelevated
                class="col"
              />
            </div>

            <div class="row q-gutter-sm">
              <q-btn
                @click="getDigitado('4')"
                label="4"
                flat
                unelevated
                class="col bg-grey-7"
              />
              <q-btn
                @click="getDigitado('5')"
                label="5"
                flat
                unelevated
                class="col bg-grey-7"
              />
              <q-btn
                @click="getDigitado('6')"
                label="6"
                flat
                unelevated
                class="col bg-grey-7"
              />
              <q-btn
                @click="metodoSubtrair"
                label="-"
                color="primary"
                flat
                unelevated
                class="col"
              />
            </div>

            <div class="row q-gutter-sm">
              <q-btn
                @click="getDigitado('1')"
                label="1"
                flat
                unelevated
                class="col bg-grey-7"
              />
              <q-btn
                @click="getDigitado('2')"
                label="2"
                flat
                unelevated
                class="col bg-grey-7"
              />
              <q-btn
                @click="getDigitado('3')"
                label="3"
                flat
                unelevated
                class="col bg-grey-7"
              />
              <q-btn
                @click="metodoSomar"
                label="+"
                color="primary"
                flat
                unelevated
                class="col"
              />
            </div>

            <div class="row q-gutter-sm">
              <q-btn
                @click="getDigitado('0')"
                label="0"
                flat
                unelevated
                class="col-6 bg-grey-7"
              />
              <q-btn
                @click="ponto"
                label="."
                flat
                unelevated
                class="col bg-grey-7"
              />
              <q-btn
                @click="metodoCalcularOperacao"
                label="="
                color="positive"
                flat
                unelevated
                class="col"
              />
            </div>
          </div>
        </q-card>
      </q-page>
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from "vue";

// variáveis
const display = ref("");
const operadorClicado = ref(false);
const operador = ref(null);
const resultadoClick = ref(null);

// métodos
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
  if (!display.value.includes(".")) {
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
.q-page {
  background-color: black;
  height: 100vh;
}
.q-card {
  max-width: 320px;
}
</style>
