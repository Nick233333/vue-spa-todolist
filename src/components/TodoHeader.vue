<template>
    <h3>My todolist<span class="badge badge-secondary float-right">{{ count }}</span></h3>
</template>

<script>
export default {
    name: 'TodoHeader',
    props: ['todos'],
    computed: {
        count() {
            if (this.todos.length === 0) {
              return;
        }
            return this.todos.length;
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
