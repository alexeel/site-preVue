<template>
  <div>
    <input
      type="text"
      class="todo-input"
      placeholder="What needs to be done"
      v-model="newTodo"
      @keyup.enter="addTodo"
    />
    <transition-group
      name="fade"
      enter-active-class="animated fadeInUp"
      leave-active-class="animated fadeOutDown"
    >
      <div
        v-for="(todo, index) in todosFiltered"
        :key="todo.id"
        class="todo-item"
      >
        <label class="todo-item-left">
          <input type="checkbox" v-model="todo.completed" />
          <div
            v-if="!todo.editing"
            @dblclick="editTodo(todo)"
            class="todo-item-label"
            :class="{ completed: todo.completed }"
          >
            {{ todo.title }}
          </div>
          <input
            v-else
            class="todo-item-edit"
            type="text"
            v-model="todo.title"
            @blur="doneEdit(todo)"
            @keyup.enter="doneEdit(todo)"
            @keyup.esc="cancelEdit(todo)"
            v-focus
          />
        </label>
        <div class="remove-item" @click="removeTodo(index)">&times;</div>
      </div>
    </transition-group>

    <div class="extra-container">
      <label class="todo-item-left"
        ><input
          type="checkbox"
          :checked="!anyRemaining"
          @change="checkAllTodos"
        />
        <span class="todo-item-label">Check All</span>
      </label>
      <div>{{ remaining }} items left</div>
    </div>

    <div class="extra-container">
      <div>
        <button :class="{ active: filter == 'all' }" @click="filter = 'all'">
          All
        </button>
        <button
          :class="{ active: filter == 'active' }"
          @click="filter = 'active'"
        >
          Active
        </button>
        <button
          :class="{ active: filter == 'completed' }"
          @click="filter = 'completed'"
        >
          Completed
        </button>
      </div>

      <div>
        <transition name="fade">
          <button v-if="showClearCompletedButton" @click="clearCompleted">
            Clear Completed
          </button>
        </transition>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "todo-list",
  data() {
    return {
      newTodo: "",
      idForTodo: 4,
      beforeEditCache: "",
      filter: "all",
      todos: [
        {
          id: 1,
          title: "Create a Vue website",
          completed: true,
          editing: false,
        },
        {
          id: 2,
          title: "Post a resume",
          completed: true,
          editing: false,
        },
        {
          id: 3,
          title: "Pass an interview",
          completed: false,
          editing: false,
        },
      ],
    };
  },
  computed: {
    remaining() {
      return this.todos.filter((todo) => !todo.completed).length;
    },
    anyRemaining() {
      return this.remaining != 0;
    },
    todosFiltered() {
      if (this.filter == "all") {
        return this.todos;
      } else if (this.filter == "active") {
        return this.todos.filter((todo) => !todo.completed);
      } else if (this.filter == "completed") {
        return this.todos.filter((todo) => todo.completed);
      }
      return this.todos;
    },
    showClearCompletedButton() {
      return this.todos.filter((todo) => todo.completed).length > 0;
    },
  },
  directives: {
    focus: {
      inserted: function (el) {
        el.focus();
      },
    },
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim().length == 0) {
        return;
      }
      this.todos.push({
        id: this.idForTodo,
        title: this.newTodo,
        completed: false,
        editing: false,
      });
      this.newTodo = "";
      this.idForTodo++;
    },
    editTodo(todo) {
      this.beforeEditCache = todo.title;
      todo.editing = true;
    },
    doneEdit(todo) {
      if (todo.title.trim() == "") {
        todo.title = this.beforeEditCache;
      }
      todo.editing = false;
    },
    cancelEdit(todo) {
      todo.title = this.beforeEditCache;
      todo.editing = false;
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    checkAllTodos() {
      this.todos.forEach((todo) => (todo.completed = event.target.checked));
    },
    clearCompleted() {
      this.todos = this.todos.filter((todo) => !todo.completed);
    },
  },
};
</script>

<style lang="scss" scoped>
@import url("https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.5.2/animate.min.css");

$primary-color: #c0ffee;
$secondary-color: #ebac0c;
$dark: #021c1e;
$text: #131313;
$light: #fff;
$grey: #696969;

label {
  &:last-child {
    margin-bottom: 0;
  }
}
input[type="checkbox"] {
  font-size: 1em;
  appearance: none;
  background: none;
  position: absolute;
  z-index: -1;
  opacity: 0;
  & + .todo-item-label {
    &::before,
    &::after {
      content: "";
      position: absolute;
      display: block;
    }
    &::before {
      top: 0.7em;
      left: 0;
      width: 1em;
      height: 1em;
      border: 1px solid $secondary-color;
    }
    &::after {
      top: 0.95em;
      left: 0.25em;
      width: 0.5em;
      height: 0.5em;
      transform: scale(0);
      background-color: $primary-color;
      transition: 0.2s;
    }
  }
  &:checked {
    & + .todo-item-label {
      &::after {
        transform: scale(1);
      }
    }
  }
}
.todo-input {
  width: 100%;
  padding: 0.5em 1em;
  font-size: 1.125em;
  margin-bottom: 0.8em;
  background: none;
  color: inherit;
  border: 1px solid currentColor;
  &:focus {
    outline: 0;
  }
}
.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 0.5em;
  animation-duration: 0.3s;
}
.remove-item {
  cursor: pointer;
  font-size: 1.5em;
  font-weight: 300;
  margin-left: 0.3em;
  &:hover {
    color: $primary-color;
  }
}
.todo-item-left {
  position: relative;
  cursor: pointer;
  display: flex;
  align-items: center;
  flex: 1;
  padding-left: 1em;
  margin-bottom: 0;
  &:hover {
    color: $primary-color;
  }
}
.todo-item-label {
  padding: 0.5em;
  margin-left: 0.3em;
}
.todo-item-edit {
  font-size: 1.2em;
  margin-left: 0.5em;
  width: 100%;
  padding: 0.5em;
  border: 0;
  &:focus {
    outline: none;
  }
}
.completed {
  text-decoration: line-through;
  color: $grey;
}
.extra-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 1em;
  border-top: 1px dashed lightgrey;
  padding-top: 1em;
  margin-bottom: 1em;
}
button {
  font-size: 0.8em;
  background: none;
  appearance: none;
  color: inherit;
  transition: 0.4s;
  border: 0;
  &:hover {
    color: $primary-color;
  }
  &:focus {
    outline: none;
  }
  &.active {
    background: $primary-color;
    color: $dark;
  }
}
// CSS Transitions
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>