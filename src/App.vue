<template>
  <div>
      <h1>{{ title }}</h1>
      <form class="search-box" @submit.prevent="addTodo">
        <input class="search-bar" v-model="query" type="text" name="todo" placeholder="Enter new task..">
        <!-- <div class="container">
          <div class="button-style">
            <button type="submit" name="button">Add</button>
            <button type="submit" name="button">All Done</button>
          </div>
        </div> -->
        <button class="add-button" type="submit" name="button">Add</button>
      </form>
      <button class="add-button" @click="allDone" type="button" name="button">All Done</button>
      <ul>
        <li class="list" v-for="todo in todos" :key="todo">
          <p :class="{ done: todo.done }">
            <label class="container">
            <input type="checkbox" v-model="todo.done"> {{ todo.title }}
            <span class="checkmark"></span>
            </label>  
          </p>
          <div class="element-button">
            <button @click="removeTodo(todo)" type="button" name="button">Remove</button>
            <button @click="addnew(todo, query)" type="submit" name="addBelow">Add Below</button>
          </div>
          </li>
      </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      title: 'Simple ToDo!!',
      query: '',
      todos: []
    }
  },
  methods: {
    addTodo() {
      this.todos.push({
        title: this.query,
        done: false
      });
      this.query = '';
    },
    removeTodo(todo) {
      let todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
    },
    allDone() {
      this.todos.forEach((todo)=> {
        todo.done = true
      });
    },
    addnew(todo, query) {
      let todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex+1, 0, query);
    }
  }
}
</script>

<style>
  body {
    background-color: aqua;
    color: rgb(66, 66, 66);
    width: 50%;
    margin: auto;
  }
  h1 {
    text-align: center;
    text-decoration: underline;
    font-family: sans-serif;
    font-style: italic;
  }
  .search-box .search-bar {
    display: block;
    width: 80%;
    height: 50px;
    margin-left: auto;
    margin-right: auto;
    font-style: italic;
    margin-top: 30px;
    font-size: 20px;
    appearance: none;
    outline: none;
    border-radius: 0px 16px 0px 16px;
    transition: 0.4s;
  }
  .search-box .search-bar:focus {
    border-radius: 16px 0px 16px 0px;
    background-color: rgba(255, 255, 255, 0.5);
  }
  .button-style {
    margin: auto;
    display: block;
    width: 50%;
    font-family: sans-serif;
    margin-top: 20px;
    height: 40px;
    font-size: 15px;
    align-items: center;
    justify-content: center;
    position: absolute;
  }
  .list {
  font-family: sans-serif;
  display: block;
  font-size: 2em;
  margin: auto;
  width: 57%;
  }
  .done {
    text-decoration: line-through;
    color: transparent;
    opacity: 90%;
    text-shadow: 0 0 5px rgba(0, 0, 0, 0.75);
  }
  /* .container {
    height: 200px;
    position: relative;
  } */
  .add-button {
    margin: auto;
    display: block;
    width: 50%;
    font-family: sans-serif;
    margin-top: 20px;
    height: 40px;
    font-size: 15px;
  }
  .checkmark {
    top: 0;
    left: 0;
    height: 25px;
    width: 25px;
    background-color: #eee;
  }
  .element-button {
    /* position: flexible;
    display: block; */
    height: auto;
    width: auto;
  }
</style>
