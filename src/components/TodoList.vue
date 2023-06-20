<template>
    <div v-if="isEdite" :class="[todo.isCompleted ? 'todo__list--completed todo__list todo__list__edite' : 'todo__list__edite todo__list']" >
      <input class="todo__list--input" v-model="todo.title"/>
      <input class="todo__list--input" v-model="todo.description"/>
      <button
          class="btn"
          @click="saveTodo(index)"
      >
      save
      </button>
      <button
          class="btn"
          @click="editeFalse"
      >
      cancel
      </button>
    </div>
    <div v-else :class="[todo.isCompleted ? 'todo__list--completed todo__list' : 'todo__list']" >
      <svg stroke="currentColor"
           fill="currentColor" stroke-width="0" viewBox="0 0 24 24" class="icon icon-check"
           height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"
           @click="toggleDone"
      >
        <g>
          <path fill="none" d="M0 0h24v24H0z"></path>
          <path
              d="M12 22C6.477 22 2 17.523 2 12S6.477 2 12 2s10 4.477 10 10-4.477 10-10 10zm0-2a8 8 0 1 0 0-16 8 8 0 0 0 0 16zm-.997-4L6.76 11.757l1.414-1.414 2.829 2.829 5.656-5.657 1.415 1.414L11.003 16z"></path>
        </g>
      </svg>
      <div class="todo__list--content">
        <h2 class="todo__list--title">{{todo.title}}</h2>
        <h3 class="todo__list--description">{{todo.description}}</h3>
      </div>
      <div class="todo__list--right">
        <svg
            stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 24 24"
            class="icon icon-delete"
             height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"
            @click="removeTodo(index)"
        >
          <g>
            <path fill="none" d="M0 0h24v24H0z"></path>
            <path
                d="M17 6h5v2h-2v13a1 1 0 0 1-1 1H5a1 1 0 0 1-1-1V8H2V6h5V3a1 1 0 0 1 1-1h8a1 1 0 0 1 1 1v3zm1 2H6v12h12V8zm-9 3h2v6H9v-6zm4 0h2v6h-2v-6zM9 4v2h6V4H9z"></path>
          </g>
        </svg>
        <svg stroke="currentColor"
             fill="currentColor"
             stroke-width="0"
             viewBox="0 0 24 24" class="icon icon-edit"
             @click="editeTrue"
             height="1em" width="1em" xmlns="http://www.w3.org/2000/svg">
          <g>
            <path fill="none" d="M0 0h24v24H0z"></path>
            <path
                d="M15.728 9.686l-1.414-1.414L5 17.586V19h1.414l9.314-9.314zm1.414-1.414l1.414-1.414-1.414-1.414-1.414 1.414 1.414 1.414zM7.242 21H3v-4.243L16.435 3.322a1 1 0 0 1 1.414 0l2.829 2.829a1 1 0 0 1 0 1.414L7.243 21z"></path>
          </g>
        </svg>
      </div>
    </div>
</template>

<script>
export default {
  name: 'TodoList',
  data() {
    return {
      isDone: false,
      isEdite: false,
    };
  },
  props: {
    todo: {
      type: Object,
      default() {
        return {}
      }
    },
    removeTodo: {
      type: Function,
      default() {
        return {}
      }
    },
    index: {
      type: Number,
      default() {
        return {}
      }
    },
  },
  methods: {
    toggleDone() {
      this.todo.isCompleted = !this.todo.isCompleted;
    },
    editeTrue() {
      this.isEdite = true;
    },
    editeFalse() {
      this.isEdite = false;
    },
    saveTodo() {
      if (this.todo.title !== '' && this.todo.description !== '') {
        const data = {
          title: this.todo.title,
          description: this.todo.description,
        }
        this.isEdite = false;
        this.$emit('saveTodo', data);
      }
    }
  },
};
</script>

<style scoped lang="scss">
@import "../styles/variables";

.todo__list {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: $color-red-bg;
  border-radius: 20px;
  color: #fff;
  padding: 12px;
  box-sizing: border-box;

  &--content {
    text-align: center;
  }

  &--title {
    font-weight: 700;
    font-size: 24px;
    white-space: pre-wrap;
  }

  &--description {
    font-size: 22px;
    white-space: pre-wrap;
  }

  &--completed {
    opacity: .5;
  }

  &--overdue {
    .todo__list--date {
      color: #535;
    }
  }

  &--input {
    height: 24px;
    border: none;
    border-radius: 4px;
    padding: 10px;
    box-sizing: border-box;
  }

  &--right {
    margin-top: 10px;
  }

  &__edite {
    display: flex;
    flex-direction: column;
    gap: 6px;

    .todo__list--input {
      width: 100%;
    }
  }
}

.btn {
  height: 30px;
  background-color: #b80808;
  border-radius: 4px;
  box-sizing: border-box;
  padding: 0 10px;
  font-size: 16px;
  color: #fff;
}

.icon {
  min-width: 24px;
  min-height: 24px;
  cursor: pointer;

  &:hover {
    transform: scale(1.3);
  }

  &-delete {
    margin-right: 12px;
  }
}

.title--completed {
  text-align: center;
}

</style>
