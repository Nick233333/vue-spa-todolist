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
            localStorage.removeItem('vue-todolist');
            this.$emit('delete');
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
