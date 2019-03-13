<template>
    <form v-on:submit.prevent="addTodo(newTodo)" class="mt-2">
        <div class="form-row">
            <div class="col-8">
                <input ref="myInput" type="text" class="form-control" placeholder="todo title" v-model="newTodo.title" required="" />
            </div>
            <div class="col-4">
                <input type="date" class="form-control" v-model.trim="newTodo.date" />
            </div>
        </div>
        <div class="form-group mt-2">
            <button type="submit" class="btn btn-success btn-block">Add todo</button>
        </div>
    </form>
</template>

<script>
let  dayjs = require('dayjs');

export default {
    name: 'TodoForm',
    props: ['todos'],
    data() {
        return {
            num: 1,
            newTodo: {id: null, title: '', date: '', completed: false}
        }
    },
    methods: {
        addTodo(newTodo) {
            if (newTodo.title.trim() === '') {
                return;
            }
            newTodo.completed = false;
            newTodo.id = this.num++;
            if (!newTodo.date) {
                let month = dayjs().month() + 1;
                month = month > 9 ? month : ('0' + month)
                newTodo.date = `${dayjs().year()}-${month}-${dayjs().date()}`;
            }
            this.todos.push(newTodo);
            this.newTodo = {id: null, title: '', date: '', completed: false};
            this.$refs.myInput.focus();
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
