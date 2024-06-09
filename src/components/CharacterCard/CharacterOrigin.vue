<template>
  <div class="content-wrapper__section">
    <span class="content-wrapper__section_subheading">First seen in:</span>
    <span class="content-wrapper__section_answer">{{ origin }}</span>
  </div>
</template>

<script lang="ts">
import { defineComponent, toRefs, PropType } from 'vue';

export default defineComponent({
  name: 'CharacterOrigin',
  props: {
    origin: {
      type: String as PropType<string>,
      required: true,
    },
  },
  setup(props) {
    const { origin } = toRefs(props);
    return { origin };
  },
});
</script>

<style scoped>
@import './common.css';
</style>
