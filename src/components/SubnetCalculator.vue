<template>
  <div class="calculator-container">
    <h1>Калькулятор подсетей</h1>
    
    <form @submit.prevent="showResult" class="form">
      <div class="input-group">
        <label for="ip">IP-адрес:</label>
        <input 
          id="ip" 
          v-model="ip" 
          type="text" 
          placeholder="Например: 192.168.1.1"
        />
      </div>
      
      <div class="input-group">
        <label for="mask">Маска подсети:</label>
        <select id="mask" v-model="mask">
          <option 
            v-for="option in maskOptions" 
            :key="option" 
            :value="option"
          >
            {{ option }}
          </option>
        </select>
      </div>
      
      <button 
        :disabled="!isIpValid(ip)" 
        type="submit"
        class="calculate-btn"
      >
        Рассчитать
      </button>
    </form>

    <div 
      v-if="isShowResult && isIpValid(ip)" 
      class="result"
    >
      <h2>Результат</h2>
      <div>IP: {{ ip }}</div>
      <div>Маска: {{ mask }}</div>
      <div>Адрес сети: {{ getNetworkAddress(ip, mask) }}</div>
      <div>Количество адресов: {{ getAddressesCount(mask) }}</div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { MASK_OPTIONS } from '@/constants/maskOptions';
import { isIpValid, getNetworkAddress, getAddressesCount } from '@/utils/ipUtils';

// Реактивные переменные
const ip = ref('');
const mask = ref('255.255.255.255');
const isShowResult = ref(false);

// Функция для отображения результата
function showResult() {
  isShowResult.value = true;
}
</script>

<style scoped>
.calculator-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

.form {
  display: flex;
  flex-direction: column;
  gap: 16px;
  margin-bottom: 20px;
}

.input-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.input-group label {
  font-weight: bold;
}

.input-group input,
.input-group select {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
}

.calculate-btn {
  padding: 12px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s;
}

.calculate-btn:hover {
  background-color: #45a049;
}

.calculate-btn:disabled {
  background-color: #cccccc;
  cursor: not-allowed;
}

.result {
  margin-top: 32px;
  padding: 16px;
  background-color: aqua;
  border-radius: 16px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.result h2 {
  margin-top: 0;
  margin-bottom: 16px;
  color: #333;
}

.result div {
  margin-bottom: 8px;
  line-height: 1.5;
}
</style>
