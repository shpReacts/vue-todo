<template>
  <div class="todo">
    <CreateTodo @add-todo="addTodo" @check-all="checkAllTodos" />
    <TodoFooter
      :leftTodoCount="leftTodoCount"
      :displayMode="displayMode"
      @mode-change="changeMode"
      @clear-done="clearDone"
    />

    <transition-group name="todo-list" tag="ul" @before-leave="beforeLeave">
      <TodoItem
        v-for="todo in filteredTodos"
        :key="todo.id"
        :todo="todo"
        @check-todo="checkTodo"
        @delete-todo="deleteTodo"
      />
    </transition-group>
  </div>
</template>

<script>
import CreateTodo from '@/components/CreateTodo';
import TodoItem from '@/components/TodoItem';
import TodoFooter from '@/components/TodoFooter';

export default {
  name: 'Todos',
  components: { CreateTodo, TodoItem, TodoFooter },
  data() {
    return {
      todos: [],
      displayMode: 'all',
    };
  },
  computed: {
    leftTodoCount() {
      return this.todos.reduce(
        (acc, currentTodo) => (currentTodo.done ? acc : acc + 1),
        0
      );
    },
    filteredTodos() {
      switch (this.displayMode) {
        case 'all':
          return this.todos;
        case 'active':
          return this.todos.filter(todo => !todo.done);
        case 'done':
          return this.todos.filter(todo => todo.done);
        default:
          return this.todos;
      }
    },
  },
  methods: {
    addTodo(newTodoText) {
      const newTodo = {
        id: Math.floor(Math.random() * 100000),
        text: newTodoText,
        done: false,
      };

      this.todos.push(newTodo);
      this.newTodoText = '';
    },
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    checkAllTodos() {
      if (this.todos.every(todo => todo.done)) {
        this.todos = this.todos.map(todo => ({ ...todo, done: false }));
      } else {
        this.todos = this.todos.map(todo => ({ ...todo, done: true }));
      }
    },
    checkTodo(id) {
      this.todos = this.todos.map(todo =>
        todo.id === id ? { ...todo, done: !todo.done } : todo
      );
    },
    changeMode(displayMode) {
      this.displayMode = displayMode;
    },
    clearDone() {
      this.todos = this.todos.filter(todo => !todo.done);
    },
    // https://forum.vuejs.org/t/transition-group-leave-transition-w-position-absolute-jumping-to-top-left-flip/12258/4
    beforeLeave(el) {
      const { marginLeft, marginTop, width, height } = window.getComputedStyle(
        el
      );

      el.style.left = `${el.offsetLeft - parseFloat(marginLeft, 10)}px`;
      el.style.top = `${el.offsetTop - parseFloat(marginTop, 10)}px`;
      el.style.width = width;
      el.style.height = height;
    },
  },
};
</script>

<style lang="scss" scoped>
@import '@/assets/colors';

.todo {
  width: 70rem;

  ul {
    display: flex;
    flex-direction: column;
  }

  @media only screen and (max-width: 720px) {
    width: 95%;
  }
}

///////////////////
// ANIMATIONS

.todo-list-enter-from {
  opacity: 0;
  transform: translateY(50px);
}

.todo-list-leave-to {
  opacity: 0;
  transform: translateY(-50px);
}

.todo-list-leave-active {
  position: absolute;
}
</style>
