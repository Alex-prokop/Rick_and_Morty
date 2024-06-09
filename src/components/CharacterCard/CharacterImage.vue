<template>
  <div class="character-card__image-wrapper">
    <img :src="image" :alt="name" />
  </div>
</template>

<script lang="ts">
import { defineComponent, toRefs, PropType } from 'vue';

export default defineComponent({
  name: 'CharacterImage',
  props: {
    image: {
      type: String as PropType<string>,
      required: true,
    },
    name: {
      type: String as PropType<string>,
      required: true,
    },
  },
  setup(props) {
    const { image, name } = toRefs(props);
    return { image, name };
  },
});
</script>

<style scoped>
.character-card__image-wrapper {
  margin-right: 20px;
}

.character-card__image-wrapper img {
  border-radius: 10px;
  width: 100%;
  height: 100%;
  object-position: center center;
  object-fit: cover;
}
</style>
