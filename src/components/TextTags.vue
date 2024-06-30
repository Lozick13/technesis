<template>
  <div ref="tags" :class="'tags' + ' tags_' + this.alignment">
    <template v-for="(tag, index) in calculatedTags">
      <div class="tags__item" :key="index">
        <v-icon v-if="tag.icon" class="tags__icon">mdi-{{ tag.icon }}</v-icon>
        <span class="tags__label">{{ tag.text }}</span>
      </div>
      <v-icon
        class="tags__delimiter"
        :key="'delimiter-' + index"
        v-if="index !== calculatedTags.length - 1"
        >mdi-circle-small</v-icon
      >
    </template>
  </div>
</template>

<script>
export default {
  name: 'TextTags',

  data() {
    return {
      calculatedTags: [],
      containerWidth: 0,
      delimiterWidth: 0,
      tagsWidth: [],
      resizeObserver: null,
    };
  },

  props: {
    tags: {
      required: true,
      type: Array,
    },
    alignment: {
      required: true,
      type: String,
    },
  },

  created() {
    this.calculatedTags = this.tags;
  },

  mounted() {
    this.containerWidth = this.$refs.tags.clientWidth;
    this.delimiterWidth = this.$el.querySelector('.tags__delimiter').clientWidth;
    this.$el.querySelectorAll('.tags__item').forEach(el => {
      this.tagsWidth.push(el.clientWidth);
    });

    this.resizeObserver = new ResizeObserver(() => {
      this.containerWidth = this.$refs.tags.clientWidth;
      this.updateTags();
    });

    this.resizeObserver.observe(this.$refs.tags);
  },

  methods: {
    updateTags() {
      let totalWidth = 0;
      const visibleTags = [];

      for (let i = 0; i < this.tags.length; i++) {
        const tagWidth = this.tagsWidth[i];
        const delimiterWidth =
          i === this.calculatedTags.length - 1 ? 0 : this.delimiterWidth + 20;
        totalWidth += tagWidth + delimiterWidth;

        if (totalWidth <= this.containerWidth) {
          visibleTags.push(this.tags[i]);
        } else {
          break;
        }
      }

      if (visibleTags.length > 0) {
        this.calculatedTags = visibleTags;
      }
    },
  },
};
</script>

<style scoped lang="scss">
.tags {
  overflow: hidden;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  gap: 10px;

  &_left {
    justify-content: flex-start;
  }

  &_width {
    justify-content: space-between;
  }

  &__item {
    display: flex;
    align-items: center;
    gap: 5px;
  }

  &__icon,
  &__delimiter,
  &__label {
    font-size: inherit;
    color: inherit;
  }
}
</style>
