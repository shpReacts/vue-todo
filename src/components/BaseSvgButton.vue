<template>
  <button class="btn" :class="$attrs.class" v-bind="$attrs">
    <img :src="svgSrc" :alt="alt" />
  </button>
</template>

<script>
export default {
  name: 'BaseSvgButton',
  inheritAttrs: false,
  props: {
    svgSrc: {
      type: String,
      required: true,
    },
    alt: {
      type: String,
      default: '',
    },
  },
};
</script>

<style lang="scss" scoped>
.btn {
  display: flex;
  align-items: center;
  padding: 1rem;
  cursor: pointer;
  border: none;
  background: inherit;
  transition: background-color 0.5s;

  img {
    height: 3rem;
    width: 3rem;
  }
}
</style>
