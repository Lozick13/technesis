<template>
  <div class="text-blocks">
    <div class="text-blocks__container">
      <span class="text-blocks__label">100% --- left</span>
      <TextTags
        class="text-blocks__tags"
        :tags="[
          { text: 'JS', icon: 'tag' },
          { text: '4.5' },
          { text: 'Ворота' },
          { text: 'Лексус', icon: 'car' },
        ]"
        :alignment="'left'"
      />
    </div>
    <div class="text-blocks__container">
      <span class="text-blocks__label">100% --- width</span>
      <TextTags
        class="text-blocks__tags"
        :tags="[
          { text: 'JS', icon: 'tag' },
          { text: '4.5' },
          { text: 'Ворота' },
          { text: 'Лексус', icon: 'car' },
        ]"
        :alignment="'width'"
      />
    </div>
    <div class="text-blocks__container">
      <span class="text-blocks__label">50% --- left</span>
      <TextTags
        class="text-blocks__tags text-blocks__tags_half"
        :tags="[
          { text: 'JS', icon: 'tag' },
          { text: '4.5' },
          { text: 'Ворота' },
          { text: 'Лексус', icon: 'car' },
        ]"
        :alignment="'left'"
      />
    </div>
    <div class="text-blocks__container">
      <span class="text-blocks__label">50% --- width</span>
      <TextTags
        class="text-blocks__tags text-blocks__tags_half"
        :tags="[
          { text: 'JS', icon: 'tag' },
          { text: '4.5' },
          { text: 'Ворота' },
          { text: 'Лексус', icon: 'car' },
        ]"
        :alignment="'width'"
      />
    </div>
  </div>
</template>

<script>
import TextTags from './components/TextTags.vue';

export default {
  name: 'App',

  components: {
    TextTags,
  },
};
</script>

<style scoped lang="scss">
.text-blocks {
  display: flex;
  flex-direction: column;
  gap: 35px;

  &__container {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  &__label {
    font-size: 1.5em;
  }

  &__tags {
    font-size: 2em;
    box-sizing: border-box;
    width: 100%;
    padding: 5px;
    border: 2px black solid;

    &_half {
      width: 50%;
    }
  }
}
</style>
