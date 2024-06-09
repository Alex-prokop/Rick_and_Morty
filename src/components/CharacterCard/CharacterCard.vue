<template>
  <article class="character-card">
    <CharacterImage :image="character.image" :name="character.name" />
    <div class="character-card__content-wrapper">
      <CharacterInfo
        :name="character.name"
        :status="character.status"
        :species="character.species" />
      <CharacterLocation :location="character.location.name" />
      <CharacterOrigin :origin="character.origin.name" />
    </div>
  </article>
</template>

<script>
import { defineComponent } from 'vue';
import CharacterImage from './CharacterImage.vue';
import CharacterInfo from './CharacterInfo.vue';
import CharacterLocation from './CharacterLocation.vue';
import CharacterOrigin from './CharacterOrigin.vue';

export default defineComponent({
  name: 'CharacterCard',
  components: {
    CharacterImage,
    CharacterInfo,
    CharacterLocation,
    CharacterOrigin,
  },
  props: {
    character: {
      type: Object,
      required: true,
    },
  },
});
</script>

<style>
.character-card {
  width: 600px;
  height: 220px;
  display: flex;
  background-color: rgb(60, 62, 68);
  overflow: hidden;
  border-radius: 0.5rem;
  margin: 0.75rem;
  margin-bottom: 20px;
  color: #ecf0f1;
}
</style>
