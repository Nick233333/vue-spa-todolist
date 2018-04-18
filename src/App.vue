<template>
  <div class="container mt-2" id="app">
    <div class="row">
      <div class="col-md-10 offset-md-1">
        <div class="card">
          <div class="card-header bg-primary text-white">
            <todo-header :todos="todos"></todo-header>  
          </div>
          <div class="card-body">
            <todo-form :todos="todos"></todo-form>
            <todo-items :todos="todos"></todo-items>
          </div>
          <div class="card-footer text-muted">
            <todo-footer :todos="todos" @delete="clearAll"></todo-footer> 
          </div>
        </div>
      </div>
    </div>
    <footer class="row m-3">
      <div class="col-md-8 offset-md-2 text-center">
        <svg class="pt-1" style="width: 1em;height: 1em; fill: red;" viewBox="0 0 1129 1024" width="100%" height="100%"><path d="M1121.5523043635708 389.36840817526297c0 309.6088452874448-555.2433879052447 630.6913926013402-555.2433879052447 630.6913926013402S11.056382484363212 698.9790832718344 11.056382484363212 389.36840817526297c0-12.845716526143347 0.005488435074405064-28.550712242104957 0.005488435074405064-41.13483155528045 0-10.53524412850656-0.005488435074405064-18.130717311726507-0.005488435074405064-28.964145904986903C11.056382484363212 145.11502711817906 150.88663607021596 3.940199223396746 323.3836463895569 3.940199223396746c98.17588623058481 0 185.65920443997885 45.82346241905164 242.9197826259993 117.33835888269431C623.5566889573757 49.76366164244831 711.0454956018439 3.940199223396746 809.2158933973546 3.940199223396746c172.49883913616273 0 312.3272639051936 141.17482789478228 312.3272639051936 315.32923248390335 0 10.8334285932604 0.007317251896341158 18.42341433371024 0.007317251896341158 28.964145904986903C1122.5218610782254 360.8176959331581 1121.5523043635708 376.5226916491196 1121.5523043635708 389.36840817526297L1121.5523043635708 389.36840817526297z"></path></svg>
        <a href="https://wp.hellocode.name" target="_blank" class="text-dark">Designed by Nick</a>
      </div>
    </footer>
  </div>
</template>

<script>
import todoHeader from './components/todoHeader'
import todoForm from './components/todoForm'
import todoItems from './components/todoItems'
import todoFooter from './components/todoFooter'

const STORAGE_KEY = 'vue-todolist';
    let todoStorage = {
      fetch() {
        let todos = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]');
        if (todos.length === 0) {
          return [];
        }
        todos.forEach((todo, index) => {
          todo.id = index;
        })
        return todos;
      },
      save(todos) {
        localStorage.setItem(STORAGE_KEY, JSON.stringify(todos));
      },
      clear() {
        localStorage.removeItem(STORAGE_KEY);
      }
    };

export default {
  name: 'App',
  components: {
    todoHeader,todoForm,todoItems,todoFooter
  },
  data() {
    return {
      todos: todoStorage.fetch(),
    }
    
  },
  watch: {
    todos: {
      handler(todos) {
      todoStorage.save(todos);
    },
    deep: true,
    }
  },
  methods: {
    clearAll() {
      this.todos = [];
    }
  }
}
</script>

<style>
    .list-group {
        height: 400px;
        overflow-y: auto;
    }
    [v-cloak] { display: none }
</style>
