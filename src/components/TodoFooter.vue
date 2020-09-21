<template>
  <div class="todo-footer">
    <span>{{ leftTodoCount }} items left</span>
    <div class="todo-footer__actions">
      <button
        class="btn"
        :class="{ active: displayMode === 'all' }"
        @click="$emit('mode-change', 'all')"
      >
        all
      </button>
      <button
        class="btn"
        :class="{ active: displayMode === 'active' }"
        @click="$emit('mode-change', 'active')"
      >
        active
      </button>
      <button
        class="btn"
        :class="{ active: displayMode === 'done' }"
        @click="$emit('mode-change', 'done')"
      >
        done
      </button>
    </div>
    <button class="btn" @click="$emit('clear-done')">
      clear done
    </button>
  </div>
</template>

<script>
export default {
  name: 'TodoFooter',
  props: {
    leftTodoCount: {
      type: [Number, String],
      required: true,
    },
    displayMode: {
      type: String,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
@import '@/assets/colors';

.todo-footer {
  background-color: $color-vue-blue-dark;
  font-size: 1.4rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 3px solid $color-vue-green;

  span {
    margin-left: 1.5rem;
  }
}

.btn {
  padding: 1.5rem;
  cursor: pointer;
  color: $color-react-sky-blue;
  font-family: inherit;
  background-color: transparent;
  border: none;
  transition: background-color 0.5s ease;
  font-size: inherit;

  &:focus,
  &:hover {
    background-color: $color-vue-blue-light;
  }

  &:focus {
    outline: 1px solid $color-vue-green;
    outline-offset: -1px;
  }

  @media only screen and (max-width: 440px) {
    padding: 1rem;
  }
}

.active {
  box-shadow: inset 0 0 10px $color-react-sky-blue;
  background-color: $color-vue-blue-light;
  text-transform: uppercase;
}
</style>
