<template>
  <div class="pagination">
    <button
      @click="changePage(info?.prev ?? null)"
      :disabled="!info?.prev"
      class="pagination-button">
      Previous
    </button>
    <button
      @click="changePage(info?.next ?? null)"
      :disabled="!info?.next"
      class="pagination-button">
      Next
    </button>
  </div>
</template>

<script setup lang="ts">
import { Info } from '../../types/Character';

defineProps<{
  info: Info | null;
}>();

const emit = defineEmits(['changePage']);

const changePage = (url: string | null) => {
  if (url) {
    const page = new URL(url).searchParams.get('page');
    if (page) {
      emit('changePage', parseInt(page, 10));
    }
  }
};
</script>

<style scoped>
.pagination {
  display: flex;
  justify-content: center;
  gap: 10px;
  padding: 20px 0;
  background: rgb(39, 43, 51);
}

.pagination-button {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  background-color: #32a64d;
  color: white;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.pagination-button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

.pagination-button:not(:disabled):hover {
  background-color: #18aa7b;
}
</style>
