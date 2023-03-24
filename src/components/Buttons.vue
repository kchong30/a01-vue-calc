<template>
    <div class="keys">
      <button @click="handleClick('7')">7</button>
      <button @click="handleClick('8')">8</button>
      <button @click="handleClick('9')">9</button>
      <button @click="handleClick('/')">÷</button>
      <button @click="handleClick('4')">4</button>
      <button @click="handleClick('5')">5</button>
      <button @click="handleClick('6')">6</button>
      <button @click="handleClick('*')">x</button>
      <button @click="handleClick('1')">1</button>
      <button @click="handleClick('2')">2</button>
      <button @click="handleClick('3')">3</button>
      <button @click="handleClick('-')">-</button>
      <button @click="handleClick('0')">0</button>
      <button @click="handleClick('.')">.</button>
      <button @click="handleClick('=')">=</button>
      <button @click="handleClick('+')">+</button>
      <button @click="handleClick('+/-')">+/-</button>
      <button @click="handleClick('%')">%</button>
      <button @click="handleClick('√')">√</button>
      <button @click="handleClick('MS')">MS</button>
      <button @click="handleClick('MR')">MR</button>
      <button @click="handleClick('MC')">MC</button>
      <button @click="handleClick('M+')">M+</button>
      <button @click="handleClick('M-')">M-</button>
      <button @click="handleClick('AC')">AC</button>
      <button @click="handleClick('C')">C</button>
    </div>
  </template>
  
  <script>
  export default {
    methods: {
      handleClick(value) {
        this.$emit("buttonClick", value);
      },
    },
  };
  </script>