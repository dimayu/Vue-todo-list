<template>
  <main :class="[isGrid ? 'todo-grid todo' : 'todo']" >
    <div class="wrapper">
      <header class="todo__header">
        <button class="todo__header--btn" @click="toggleGrid">
          <span></span>
          <span></span>
          <span></span>
          <span></span>
        </button>
        <h1 class="todo__header--title">My Tasks</h1></header>
      <div class="todo-wrapper">
        <TodoList
            v-for="(todo, index) in todos"
            :key="todo.id"
            v-bind:todo="todo"
            v-bind:index="index"
            v-bind:removeTodo="removeTodo"
            @saveTodo="saveTodo"
        />
      </div>
      <FormTodo @getTodo="getTodo"/>
    </div>
  </main>
</template>

<script>
import FormTodo from '@/components/FormTodo.vue';
import TodoList from '@/components/TodoList.vue';

export default {
  name: 'HomeView',
  components: {
    FormTodo,
    TodoList,
  },
  data() {
    return {
      todos: [],
      todo: {
        id: '',
        title: '',
        description: '',
        isCompleted: false,
      },
      isGrid: false,
    };
  },
  mounted() {
    const data = localStorage.getItem('todos');
    data ? this.todos = JSON.parse(data) : null;
  },
  methods: {
    getTodo(data) {
      this.todo = data;
      this.todos.push(this.todo);
      localStorage.setItem('todos', JSON.stringify(this.todos));
    },
    toggleGrid() {
      this.isGrid = !this.isGrid;
    },
    removeTodo(index) {
      this.$delete(this.todos, index)
      localStorage.setItem('todos', JSON.stringify(this.todos));
    },
    saveTodo(index, data) {
      this.todos.map((todo) => {
        return todo.index === index
            ? {...todo, title: data.title, description: data.description}
            : {...todo}
      });
      localStorage.setItem('todos', JSON.stringify(this.todos));
    }
  },
  computed: {
  }
};
</script>

<style scoped lang="scss">
@import "../styles/variables";

.todo__header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 30px;

  &--btn {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    width: 30px;
    height: 30px;
    padding: 0;

    .todo-grid & {

      span {
        width: 100%;
        height: 3px;

        &:nth-child(2) {
          margin: 2px 0;
        }

        &:last-child {
          display: none;
        }
      }
    }

    span {
      width: 45%;
      height: 45%;
      border-radius: 2px;
      background-color: $color-red;
      transition: all .1ms;
    }
  }

  &--title {
    font-weight: 700;
    font-size: 32px;
  }
}

.todo-wrapper {
  max-height: calc(60vh - 76px);
  overflow-y: auto;
}
</style>
