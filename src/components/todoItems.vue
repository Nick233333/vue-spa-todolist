<template>
    <ul class="list-group">
        <li class="list-group-item" v-for="(todo, index) in todos">
            <div v-if="todo.completed">
                <del>{{ todo.title }} -- {{ todo.date }}</del>
                <button v-on:click="deleteTodo(index)" type="button" class="btn btn-sm btn-danger float-right" aria-label="Close">
                    <span aria-hidden="true">&times;</span>
                </button>
                <button v-on:click="updateTodo(todo)" type="button" class="btn btn-sm btn-success text-white float-right mr-2">
                    <span aria-hidden="true">{{ todo.completed ? '已完成' : '未完成' }}</span>
                </button>
            </div>
            <div v-else>{{ todo.title }} -- {{ todo.date }}
                <button v-on:click="deleteTodo(index)" type="button" class="btn btn-sm btn-danger float-right" aria-label="Close">
                    <span aria-hidden="true">&times;</span>
                </button>
                <button v-on:click="updateTodo(todo)" type="button" class="btn btn-sm btn-warning text-white float-right mr-2">
                    <span aria-hidden="true">{{ todo.completed ? '已完成' : '未完成' }}</span>
                </button>
            </div>
        </li>
    </ul>
</template>

<script>
export default {
    name: 'todoItems',
    props: ['todos'],
    methods: {
        deleteTodo(index) {
            this.todos.splice(index, 1);
        },
        updateTodo(todo) {
            todo.completed = !todo.completed;
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
