<template>
  <li class="todo-item">
    <BaseSvgButton
      class="todo-item__btn"
      @click="$emit('check-todo', todo.id)"
      :svgSrc="todo.done ? doneIcon : notDoneIcon"
      :alt="todo.done ? 'done' : 'yet to be done'"
    />
    <span
      class="todo-item__text"
      :class="{ 'todo-item__text--done': todo.done }"
    >
      {{ todo.text }}
    </span>
    <BaseSvgButton
      class="todo-item__btn"
      @click="$emit('delete-todo', todo.id)"
      :svgSrc="deleteIcon"
      alt="delete"
    />
  </li>
</template>

<script>
import BaseSvgButton from '@/components/BaseSvgButton';

import doneIcon from '@/assets/checkbox.svg';
import notDoneIcon from '@/assets/checkbox_outline.svg';
import deleteIcon from '@/assets/delete.svg';

export default {
  name: 'TodoItem',
  components: {
    BaseSvgButton,
  },
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      doneIcon,
      notDoneIcon,
      deleteIcon,
    };
  },
};
</script>

<style lang="scss" scoped>
@import '@/assets/colors';

.todo-item {
  display: flex;
  align-items: center;
  padding: 1rem 0;
  background-color: $color-vue-blue-dark;
  transition: all 1s;

  &__text {
    flex: 1;
    font-size: 1.8rem;
    word-break: break-all;

    &--done {
      font-style: italic;
      text-decoration: line-through;
      color: $color-vue-blue-light;
    }
  }

  &__btn {
    display: flex;
    align-items: center;
    padding: 1rem;
    cursor: pointer;
    border: none;
    background: inherit;

    img {
      height: 3rem;
      width: 3rem;
    }
  }

  &:not(:last-of-type) {
    border-bottom: 1px solid $color-vue-green;
  }
}
</style>
