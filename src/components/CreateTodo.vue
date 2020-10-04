<template>
  <div class="create-todo">
    <input
      class="create-todo__input"
      type="text"
      placeholder="What needs to be done?"
      v-model.trim="newTodoText"
      @keydown.enter="addTodo"
    />
    <BaseSvgButton
      class="create-todo__btn"
      @click="addTodo"
      :svgSrc="plusIcon"
      alt="check all"
    />
  </div>
</template>

<script>
import BaseSvgButton from '@/components/BaseSvgButton';

import plusIcon from '@/assets/plus.svg';

export default {
  name: 'CreateTodo',
  components: { BaseSvgButton },
  data() {
    return {
      newTodoText: '',
      plusIcon,
    };
  },
  methods: {
    addTodo() {
      this.$emit('add-todo', this.newTodoText);
      this.newTodoText = '';
    },
  },
};
</script>

<style lang="scss" scoped>
@import '@/assets/colors';

.create-todo {
  display: flex;
  align-items: center;
  background-color: $color-vue-blue-dark;

  &__btn {
    &:hover,
    &:focus {
      background-color: $color-vue-blue-light;
    }

    &:focus {
      outline: 1px solid $color-vue-green;
      outline-offset: -1px;
    }
  }

  &__input {
    flex: 1;
    font-family: inherit;
    color: inherit;
    font-size: 2rem;
    align-self: stretch;
    border: none;
    background: transparent;
    padding-left: 1rem;

    &:focus {
      outline: 1px solid $color-vue-green;
      outline-offset: -1px;
    }
  }
}
</style>
