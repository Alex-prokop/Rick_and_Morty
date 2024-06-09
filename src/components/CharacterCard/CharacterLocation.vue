<template>
  <div class="content-wrapper__section">
    <span class="content-wrapper__section_subheading"
      >Last known location:</span
    >
    <span class="content-wrapper__section_answer">{{ location }}</span>
  </div>
</template>

<script lang="ts">
import { defineComponent, toRefs, PropType } from 'vue';

export default defineComponent({
  name: 'CharacterLocation',
  props: {
    location: {
      type: String as PropType<string>,
      required: true,
    },
  },
  setup(props) {
    const { location } = toRefs(props);
    return { location };
  },
});
</script>

<style scoped>
@import './common.css';
</style>
