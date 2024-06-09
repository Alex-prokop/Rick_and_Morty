<script setup lang="ts">
import { ref } from 'vue';
import Header from './components/Header.vue';
import CharacterList from './components/CharacterList.vue';

const filters = ref<{ name: string; status: string }>({ name: '', status: '' });

const applyFilter = (filterData: { name: string; status: string }) => {
  filters.value = filterData;
};
</script>

<template>
  <div>
    <Header @applyFilter="applyFilter" />
    <CharacterList :filters="filters" />
  </div>
</template>

<style></style>
