<template>
  <div class="form-field">
    <h1 class="title">I need to do!</h1>
    <input
      class="input-field"
      type="text"
      placeholder="Add new todo"
      v-model.trim="todoText"
      @keyup.enter="addTodo"
    />
    <button class="submit-btn" @click="addTodo">Submit</button>
    <ul>
      <li
        :class="{ 'todo-item': !todo.isDone, 'todo-item-done': todo.isDone }"
        v-for="todo in selectedTodos"
        :key="todo.id"
      >
        <input
          class="checkbox-btn"
          v-if="todo.isDone"
          @change="checkTodo(todo.id)"
          type="checkbox"
          :value="todo.isDone"
          checked
        />

        <input
          class="checkbox-btn"
          v-if="!todo.isDone"
          @change="checkTodo(todo.id)"
          type="checkbox"
          :value="todo.isDone"
        />

        <p class="content">{{ todo.title }}</p>
        <button
          :class="{
            'cancel-btn': !todo.isDone,
            'cancel-btn-done': todo.isDone,
          }"
          @click="removeTodo(todo.id)"
        >
          <svg
            width="12"
            height="12"
            viewBox="0 0 50 50"
            xmlns="http://www.w3.org/2000/svg"
            class="icon"
          >
            <g>
              <path
                d="M45.363,36.234l-13.158-13.16l12.21-12.21c2.31-2.307,2.31-6.049,0-8.358c-2.308-2.308-6.05-2.307-8.356,0l-12.212,12.21
		L11.038,1.906c-2.309-2.308-6.051-2.308-8.358,0c-2.307,2.309-2.307,6.049,0,8.358l12.81,12.81L1.732,36.831
		c-2.309,2.31-2.309,6.05,0,8.359c2.308,2.307,6.049,2.307,8.356,0l13.759-13.758l13.16,13.16c2.308,2.308,6.049,2.308,8.356,0
		C47.673,42.282,47.672,38.54,45.363,36.234z"
              />
            </g>
          </svg>
        </button>
      </li>
    </ul>
    <p class="item-counter" v-if="todos.length !== 0">
      {{ notDoneCounter }} item<span
        v-if="todos.length > 1 && allActive.length > 1"
        >s</span
      >
      left
    </p>

    <div v-if="allCompleted.length !== 0" class="control-btns">
      <button
        class="option"
        :class="{ all: returnState === 'all' }"
        @click="returnState = 'all'"
        v-if="todos.length !== 0"
      >
        All
      </button>
      <button
        @click="returnState = 'completed'"
        class="option"
        :class="{ completed: returnState === 'completed' }"
      >
        Completed
      </button>
      <button
        @click="returnState = 'active'"
        class="option"
        :class="{ active: returnState === 'active' }"
      >
        Active
      </button>
      <button @click="clearAllCompleted" class="option">Clear completed</button>
    </div>
    <div class="empty-todos" v-if="todos.length === 0">
      <p>You have no more tasks to do</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todoText: "",
      todos: [],
      returnState: "all",
    };
  },
  methods: {
    addTodo() {
      if (!this.todoText || this.todoText === " ") return;
      const todosLength = this.todos.length;
      const nextId = todosLength ? this.todos[todosLength - 1].id + 1 : 1;
      this.todos.push({
        id: nextId,
        title: this.firstLetterUpperTodoText,
        isDone: false,
      });

      this.todoText = "";
    },
    removeTodo(id) {
      this.todos = this.todos.filter((item) => {
        return id !== item.id;
      });
    },
    checkTodo(id) {
      const foundObj = this.todos.find((el) => el.id === id);
      this.$set(foundObj, "isDone", !foundObj.isDone);
    },
    clearAllCompleted() {
      this.todos = this.todos.filter((item) => {
        this.returnState = "all";
        return item.isDone !== true;
      });
    },
  },
  computed: {
    firstLetterUpperTodoText() {
      if (!this.todoText) {
        return;
      }
      const [firstChar, ...last] = this.todoText;
      return firstChar.toUpperCase() + last.join("");
    },
    notDoneCounter() {
      return this.todos.filter((item) => {
        return item.isDone === false;
      }).length;
    },
    allCompleted() {
      return this.todos.filter((item) => {
        return item.isDone;
      });
    },
    allActive() {
      return this.todos.filter((item) => {
        return !item.isDone;
      });
    },
    selectedTodos() {
      if (this.returnState === "all") {
        return this.todos;
      }
      if (this.returnState === "active") {
        return this.allActive;
      }
      if (this.returnState === "completed") {
        return this.allCompleted;
      }

      return [];
    },
  },
};
</script>

<style scoped>
.option:hover {
  border-radius: 4px;
  cursor: pointer;
  background-color: #557a95;
  color: white;
}

.all {
  padding: 0 0.6em;
  border-radius: 4px;
  cursor: pointer;
  background-color: #557a95;
  color: white;
}

.completed {
  padding: 0 0.6em;
  border-radius: 4px;
  cursor: pointer;
  background-color: #557a95;
  color: white;
}

.active {
  padding: 0 0.6em;
  border-radius: 4px;
  cursor: pointer;
  background-color: #557a95;
  color: white;
}

.title {
  font-size: 22px;
  margin-bottom: 18px;
  font-family: Yanone Kaffeesatz, sans-serif;
  font-weight: bold;
  color: #5d5c61;
}

.form-field {
  margin-top: 25px;
}

.completed:checked {
  background-color: aqua;
}

.input-field {
  border-bottom: 3px dashed #5d5c61;
  outline: none;
  background: transparent;
  margin-right: 15px;
  font-size: 18px;
  width: 70%;
}

.submit-btn {
  font-size: 17px;
  padding: 0.25em 0.8em 0.15em;
  color: white;
  background: #5d5c61;
  border: 2px solid #5d5c61;
  border-radius: inherit;
  position: relative;
  transform: rotate(4deg);
  border-radius: 6px;
  transition: transform 0.25s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.submit-btn:active {
  transform: translateX(4px);
}

.checkbox {
  padding: 5px;
  border-radius: 2px;
  border: 2px solid #494a4b;
}

.checkboxx {
  border-radius: 2px;
  border: 2px solid #065cb3;
}

.checkbox-btn {
  padding: 5px;
  border-radius: 5px;
  border: 2px solid #1f5488;
  outline: none;
  cursor: pointer;
  margin-left: 10px;
}

.cancel-btn {
  width: 10px;
  fill: #494a4b;
  margin: 0 -5px 0 auto;
  padding: 0 15px;
}

.cancel-btn-done {
  width: 10px;
  fill: #ffffff;
  margin: 0 -5px 0 auto;
  padding: 0 15px;
}

.cancel-btn:hover {
  fill: #a9a9aa;
}

.todo-item {
  display: flex;
  align-items: center;
  padding: 8px 10px 8px 0;
  border-radius: 5px;
  margin-top: 15px;
}

.todo-item-done {
  display: flex;
  align-items: center;
  padding: 8px 10px 8px 0;
  border-radius: 5px;
  background-color: #557a95;
  margin-top: 15px;
  animation: flip 0.75s ease-in-out both;
}

@keyframes flip {
  0% {
    transform: rotateX(90deg);
    opacity: 0;
  }
  40% {
    transform: rotateX(-10deg);
  }
  70% {
    transform: rotateX(10deg);
  }
  100% {
    transform: rotateX(0deg);
    opacity: 1;
  }
}

.empty-todos {
  margin-top: 30px;
  animation: zoom 0.45s ease-in-out;
  color: rgba(73, 74, 75, 0.45);
}

@keyframes zoom {
  0% {
    opacity: 0;
    transform: scale(0.75);
  }
  50% {
    transform: scale(1.15);
  }
  100% {
    opacity: 1;
    transform: scale(1);
  }
}

.content {
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow: hidden;
  padding-right: 7px;
  padding-left: 7px;
}

.control-btns {
  display: flex;
  justify-content: space-between;
  margin-top: 50px;
  gap: 20px;
}

.item-counter {
  margin-top: 25px;
}
</style>
