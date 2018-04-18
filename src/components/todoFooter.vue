<template>
    <div class="d-flex justify-content-between">
        <span class="float-left">已完成 {{ completed }}</span>
        <button class="btn btn-danger btn-sm w-25" @click="clear()">清空</button>
        <span class="float-right">未完成 {{ uncompleted }}</span>
    </div>
</template>

<script>
export default {
    name: 'todoFooter',
    props: ['todos'],
    computed: {
        uncompleted() {
            return this.todos.filter((todo) => {
                return todo.completed === false;
            }).length;
        },
        completed() {
            return this.todos.filter((todo) => {
                return todo.completed === true;
            }).length;
        }
    },
    methods: {
        clear() {
            todoStorage.clear();
            this.$emit('delete');
        }
    }
}
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
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
