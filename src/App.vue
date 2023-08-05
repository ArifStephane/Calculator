<template>
  <div class="flex justify-center py-40">
 <div class="  bg-black p-4 rounded-2xl shadow-md">
    <div class="flex justify-end bg-black text-white p-2 h-11 rounded mb-4 text-2xl font-semibold">{{ currentInput }}</div>
    <div class="buttons grid grid-cols-4 gap-2 ">
      <button
        v-for="calculator in calculatorKeys"
        :key="calculator"
        @click="handleButtonClick(calculator)"
        class="bg-gray-300 text-gray-700 hover:bg-gray-400 hover:text-white px-4 py-2 rounded"
      >
        {{ calculator }}
      </button>
    </div>
  </div>
  </div>
 
</template>

<script setup lang="ts">
import { ref } from 'vue';
import * as math from 'mathjs';

const currentInput = ref<string>('');
const calculatorKeys: string[] = [
  'AC', 'C', '²', 'mod',
  '7', '8', '9', '*',  
  '4', '5', '6', '-',
  '1', '2', '3', '+',
  '0', '.', '=', '/',
];

const handleButtonClick = (key: string): void => {
  switch (key) {
    case '=':
      try {
        currentInput.value = math.evaluate(currentInput.value);
      } catch (error) {
        currentInput.value = 'Error';
      }
      break;
    case 'C':
      currentInput.value = currentInput.value.slice(0, -1);
      break;
    case 'AC':
      currentInput.value = '';
      break;
       case '²':
      currentInput.value += '^2';
      break;
    case 'mod':
      currentInput.value += '%';  
      break;
    default:
      currentInput.value += key;
      break;
  }
};
</script>

<style scoped>
 
</style>
