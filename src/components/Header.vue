<template>
  <header>
    <h1>Rick and Morty</h1>
    <Filter @applyFilter="applyFilter" />
  </header>
</template>

<script setup lang="ts">
import Filter from './common/Filter.vue';

const emit = defineEmits(['applyFilter']);

const applyFilter = (filterData: { name: string; status: string }) => {
  emit('applyFilter', filterData);
};
</script>

<style>
header {
  text-align: center;
  padding: 20px;
  background-color: #282c34;
  color: white;
  margin: 0 auto;
}

h1 {
  margin: 0;
  font-size: 2em;
}
</style>
