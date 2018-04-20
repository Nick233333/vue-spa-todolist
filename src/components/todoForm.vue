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
export default {
    name: 'todoForm',
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
                let date = new Date();
                let month = date.getMonth() < 10 ? `0${date.getMonth()}` : date.getMonth();
                newTodo.date = `${date.getFullYear()}-${month}-${date.getDate()}`;
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
