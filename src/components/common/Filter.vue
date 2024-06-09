<template>
  <div class="filter">
    <input
      class="filter__input"
      v-model="name"
      placeholder="Name"
      @input="clearError" />
    <select class="filter__select" v-model="status">
      <option value="">All</option>
      <option value="alive">Alive</option>
      <option value="dead">Dead</option>
      <option value="unknown">Unknown</option>
    </select>
    <button @click="applyFilter" class="filter__button">Find</button>
  </div>
  <div v-if="error" class="error-message">{{ error }}</div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const emit = defineEmits(['applyFilter']);

const name = ref('');
const status = ref('');
const error = ref<string | null>(null);

const clearError = () => {
  error.value = null;
};

const applyFilter = () => {
  if (name.value.trim() !== '' && !/^[a-zA-Z\s]+$/.test(name.value.trim())) {
    error.value = 'Недопустимые символы в имени';
  } else {
    error.value = null;
    emit('applyFilter', { name: name.value, status: status.value });
  }
};
</script>

<style>
.filter {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
}

.filter__input,
.filter__select {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
  width: 200px;
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
}

.filter__input:focus,
.filter__select:focus {
  border-color: #007bff;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
  outline: none;
}

.filter__button {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  background-color: #32a64d;
  color: white;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.filter__button:not(:disabled):hover {
  background-color: #18aa7b;
}

.error-message {
  color: red;
  font-weight: bold;
  margin-top: 10px;
}
</style>
