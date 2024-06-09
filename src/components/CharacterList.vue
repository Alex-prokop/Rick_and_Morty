<template>
  <div>
    <div v-if="error" class="error-message">{{ error }}</div>
    <div class="character-list">
      <CharacterCard
        v-for="character in characters"
        :key="character.id"
        :character="character" />
    </div>
    <Pagination
      v-if="info && !error"
      :info="info"
      @changePage="fetchCharacters" />
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, watch } from 'vue';
import CharacterCard from './CharacterCard/CharacterCard.vue';
import Pagination from './common/Pagination.vue';
import { Character, Info } from '../types/Character';

const props = defineProps<{
  filters: { name: string; status: string };
}>();

const characters = ref<Character[]>([]);
const info = ref<Info | null>(null);
const error = ref<string | null>(null);

const fetchCharacters = async (page = 1) => {
  try {
    const params = new URLSearchParams({
      page: page.toString(),
      name: props.filters.name,
      status: props.filters.status,
    });
    const response = await fetch(
      `https://rickandmortyapi.com/api/character/?${params}`
    );
    if (!response.ok) {
      if (response.status === 404) {
        error.value = 'Введено неверное имя';
      } else {
        throw new Error(`HTTP error! status: ${response.status}`);
      }
      return;
    }
    const data = await response.json();
    characters.value = data.results;
    info.value = data.info;
    error.value = null;
  } catch (err) {
    console.error(err);
    error.value = 'Не удалось загрузить персонажей. Попробуйте позже.';
  }
};

watch(
  () => props.filters,
  () => {
    fetchCharacters();
  },
  { deep: true }
);

onMounted(() => {
  fetchCharacters();
});
</script>

<style>
.character-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin: 0 auto;
  background: rgb(39, 43, 51);
}
.error-message {
  color: red;
  text-align: center;
  margin: 20px;
}
</style>
