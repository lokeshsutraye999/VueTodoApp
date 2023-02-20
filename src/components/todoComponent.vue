<template>
  <div class="wrapper">
    <header>Todo App</header>
    <div class="inputField">
      <input type="text" placeholder="Add your new todo" v-model="task">
      <button @click.prevent="addNewTodo">+</button>
    </div>
    <ul class="todoList">
      <li v-for="(todo, index) in todos" v-bind:key="todo.isActive" :class="{ completed: todo.isActive }"
        @click="$set(todo, 'isActive', !todo.isActive)">
        {{ todo.task }} <span v-on:click="deleteTodo(index)">{{ todo.delete }}</span>
      </li>
      <li v-for="todo1 in todos1" v-bind:key="todo1" class="completed">
        {{ todo1.task }}
      </li>
    </ul>
    <div class="footer">
      <span>You have <span class="pendingTasks">{{ todos.length }}</span> pending tasks</span>
      <span>You have <span class="pendingTasks">{{ todos1.length }}</span> Completed tasks</span>
      <button @click="deleteAllTodo">Clear All</button>
    </div>
  </div>
</template>
  
<script>
export default {
  name: 'todoComponent',
  data() {
    return {
      todos: [
      ],
      todos1: [
      ],
      task: '',
    }
  },
  mounted() {
    this.todos1 = JSON.parse(localStorage.getItem("todos1"));
    this.todos = JSON.parse(localStorage.getItem("todos"));

  },
  methods: {
    /* eslint-disable */
    addNewTodo: function () {
      if (this.task != '') {
        let todo = { task: this.task, delete: '(x)' };
        this.todos.push(todo);
        localStorage.setItem("todos", JSON.stringify(this.todos));
        localStorage.setItem("todos1", JSON.stringify(this.todos1));

        this.task = ''; // clear input
      } else {
        alert("Please enter Text");
      }
    },
    deleteTodo: function (index) {
      this.todos1.push(this.todos[index]);
      this.todos.splice(index, 1);
      this.saveTasksToLocalStorage();
    },
    deleteAllTodo() {
      if (confirm('Are You Sure?')) {
        this.todos.length = 0;
        this.todos1.length = 0;
        localStorage.clear();
        this.saveTasksToLocalStorage();
      }
    },
    saveTasksToLocalStorage() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
      localStorage.setItem("todos1", JSON.stringify(this.todos1));
    }
  }
}
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;500;600;700&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Poppins', sans-serif;
}

::selection {
  color: #ffff;
  background: rgb(142, 73, 232);
}

body {
  width: 100%;
  height: 100vh;
  padding: 10px;
  background: linear-gradient(to bottom, #68EACC 0%, #497BE8 100%);
}

.wrapper {
  background: #8dd0e0;
  max-width: 400px;
  width: 100%;
  margin: 120px auto;
  padding: 25px;
  border-radius: 5px;
  box-shadow: 0px 10px 15px rgba(0, 0, 0, 0.1);
}

.wrapper header {
  font-size: 30px;
  font-weight: 600;
}

.wrapper .inputField {
  margin: 20px 0;
  width: 100%;
  display: flex;
  height: 45px;
}

.inputField input {
  width: 85%;
  height: 100%;
  outline: none;
  border-radius: 3px;
  border: 1px solid #ccc;
  font-size: 17px;
  padding-left: 15px;
  transition: all 0.3s ease;
}

.inputField input:focus {
  border-color: #8E49E8;
}

.inputField button {
  width: 50px;
  height: 100%;
  border: none;
  color: #fff;
  margin-left: 5px;
  font-size: 21px;
  outline: none;
  background: #8E49E8;
  cursor: pointer;
  border-radius: 3px;
  opacity: 0.6;
  transition: all 0.3s ease;
}

.inputField button:hover,
.footer button:hover {
  background: #0ecac1;
}

.inputField button.active {
  opacity: 1;
  pointer-events: auto;
}

.wrapper .todoList {
  max-height: 250px;
  overflow-y: auto;
}

.todoList li {
  position: relative;
  list-style: none;
  margin-bottom: 8px;
  background: #f2f2f2;
  border-radius: 3px;
  padding: 10px 15px;
  cursor: default;
  overflow: hidden;
  word-wrap: break-word;
}

.todoList li .icon {
  position: absolute;
  right: -45px;
  top: 50%;
  transform: translateY(-50%);
  background: #e74c3c;
  width: 45px;
  text-align: center;
  color: #fff;
  padding: 10px 15px;
  border-radius: 0 3px 3px 0;
  cursor: pointer;
  transition: all 0.2s ease;
}

.todoList li:hover .icon {
  right: 0px;
}

.wrapper .footer {
  display: flex;
  width: 100%;
  margin-top: 20px;
  align-items: center;
  justify-content: space-between;
}

.footer button {
  padding: 6px 10px;
  border-radius: 10px;
  border: none;
  outline: none;
  color: #fff;
  font-weight: 400;
  font-size: 16px;
  margin-left: 5px;
  background: #8E49E8;
  cursor: pointer;
  user-select: none;
  opacity: 0.6;
  transition: all 0.3s ease;
}

.footer button.active {
  opacity: 1;
  pointer-events: auto;
}

.completed {
  text-decoration: line-through;
}
</style>
  
