

<script setup>
import { ref } from 'vue';

let previous = ref(null);
let current = ref('');
let operator = ref(null);
let operatorClicked = ref(false);

const clear = () => {
      current.value = '';

};

const sign = () => {
  current.value = current.value.charAt(0) === '-' ? current.value.slice(1) : `-${current.value}`;
};

const percent = () => {
  current.value = `${parseFloat(current.value) / 100}`;
};

const append = (number) => {
  if (operatorClicked.value) {
    current.value = '';
    operatorClicked.value = false;
  }
  current.value = `${current.value}${number}`;
};

const dot = () => {
  if (current.value.indexOf('.') === -1) {
    append('.');
  }
};

const setPrevious = () => {
  previous.value = current.value;
  operatorClicked.value = true;
};

const divide = () => {
  operator.value = (a, b) => a / b;
  setPrevious();
};

const times = () => {
  operator.value = (a, b) => a * b;
  setPrevious();
};

const minus = () => {
  operator.value = (a, b) => a - b;
  setPrevious();
};

const add = () => {
  operator.value = (a, b) => a + b;
  setPrevious();
};

const equal = () => {
  current.value = `${operator.value(parseFloat(current.value), parseFloat(previous.value))}`;
  previous.value = null;
};
</script>

<template>
<div class="calculator">
    <div class="display">{{current || '0'}}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="times" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
</div>
</template>

<style scoped>
.calculator {
  margin: 0 auto;
  width: 400px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.display {
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
}

.zero {
  grid-column: 1 / 3;
}

.btn {
  background-color: #F2F2F2;
  border: 1px solid #999;
}

.operator {
  background-color: orange;
  color: white;
}
</style>
