<template>
  <div class="content-wrapper__section">
    <h2 class="content-wrapper__section_header">{{ name }}</h2>
    <span class="content-wrapper__status">
      <span :class="['status-icon', status.toLowerCase()]"></span>
      {{ status }} - {{ species }}
    </span>
  </div>
</template>

<script lang="ts">
import { defineComponent, toRefs, PropType } from 'vue';

export default defineComponent({
  name: 'CharacterInfo',
  props: {
    name: {
      type: String as PropType<string>,
      required: true,
    },
    status: {
      type: String as PropType<string>,
      required: true,
    },
    species: {
      type: String as PropType<string>,
      required: true,
    },
  },
  setup(props) {
    const { name, status, species } = toRefs(props);
    return { name, status, species };
  },
});
</script>

<style scoped>
.content-wrapper__section {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  margin: 10px 0;
}

.content-wrapper__section_header {
  display: flex;
  justify-content: flex-start;
  margin: 0;
  font-size: 1.7rem;
}

.content-wrapper__status {
  display: flex;
  align-items: center;
  color: #ecf0f1;
  text-transform: capitalize;
}
.status-icon {
  display: inline-block;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  margin-right: 5px;
}

.status-icon.alive {
  background-color: #2ecc71;
}

.status-icon.dead {
  background-color: #e74c3c;
}

.status-icon.unknown {
  background-color: #95a5a6;
}
</style>
