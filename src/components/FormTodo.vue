<template>
  <div class="todo__add">
    <button class="todo__btn-add"
            @click="show"
    >+
    </button>
    <form class="todo__form" :class="[isActive ? 'active' : '']">
      <button class="todo__form--close" @click="hide">&#9587;</button>
      <p>Todo Title</p>
      <input type="text"
             placeholder="Todo title....."
             class="todo__form--input" value=""
             v-model="todo.title"
      >
      <p>Todo Description</p>
      <input type="text"
             placeholder="Todo description....."
             class="todo__form--input" value=""
             v-model="todo.description"
      >
      <button
          class="todo__form--btn"
          @click="addTodo"
      >Save
      </button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'TodoForm',
  data() {
    return {
      todos: [],
      todo: {
        id: '',
        title: '',
        description: '',
        isCompleted: false,
      },
      isActive: false
    };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      if (this.todo.title !== '' && this.todo.description !== '') {
        this.todo.id = Date.now();
        this.$emit('getTodo', this.todo);
        this.todo = {
          id: '',
          title: '',
          description: '',
          isCompleted: false,
        };
      }
    },
    show(e) {
      e.preventDefault();
      this.isActive = true;
    },
    hide(e) {
      e.preventDefault();
      this.isActive = false;
    },
  },
};
</script>

<style scoped lang="scss">
@import "../styles/variables";

.todo__btn-add {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  bottom: 40px;
  width: 60px;
  height: 60px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 24px;
  color: #fff;
  background-color: $color-red;
  border-radius: 50%;
  filter: drop-shadow(0px 2px 4px #FF4444);

  &:hover {
    filter: none;
  }
}

.todo__form {
  position: absolute;
  bottom: 0;
  width: 100%;
  background-color: #fff;
  box-shadow: 0 -5px 4px rgba(0, 0, 0, 0.5);
  border-radius: 20px 15px 0 0;
  color: #52525C;
  padding: 20px;
  box-sizing: border-box;
  transform: translateY(100vh);
  transition: transform .7s linear;

  &--close {
    display: flex;
    margin-left: auto;
    margin-bottom: 20px;
    font-size: 24px;
    text-align: right;
    cursor: pointer;
  }

  &--title {
    text-align: center;
    margin-bottom: 10px;
    font-size: 20px;
    color: $color-red;
  }

  &--input {
    width: 100%;
    border: 2px solid #D9D9D9;
    border-radius: 10px;
    margin: 12px 0;
    padding: 12px;
    box-sizing: border-box;

    &:focus {
      outline: none;
      border: 2px solid $color-red-bg;
    }
  }

  &--btn {
    width: 100%;
    background-color: $color-red-bg;
    border-radius: 10px;
    margin-top: 20px;
    padding: 12px;
    color: #fff;
    font-size: 24px;
    border: 2px solid $color-red-bg;
    box-sizing: border-box;

    &:hover {
      background-color: #fff;
      color: $color-red-bg;
    }
  }

  &.active {
    transform: translateY(0);
    z-index: 1;
    left: 0;
  }
}
</style>
