<template>
    <div>
        <ul>
            <TodoItem 
                v-for='(todo, i) of todos'
                v-bind:todo="todo"
                v-bind:key="todo.id"
                @remove-todo='removeTodo'
                v-bind:index="i"
            />
        </ul>
    </div>
</template>

<script>
import TodoItem from '@/components/TodoItem'
export default {
    props: ['todos'],
    components: {
        TodoItem
    },
    methods: {
        removeTodo(id) {
            this.$emit('remove-todo', id)
        }
    }
}
</script>

<style scoped>
    ul {
        max-width: 400px;
        list-style: none;
        margin: 0 auto;
        padding: 0;
    }
    
</style>