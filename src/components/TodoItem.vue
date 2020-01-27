<template>
    <li>
        <div v-bind:class="{done: todo.completed}">
            <input type="checkbox" v-on:change='todo.completed = !todo.completed'>
            <span>
                <strong>{{ index + 1 }}</strong>
                {{ todo.title | uppercase }}

            </span>
        </div>
        <button class='rm' v-on:click="$emit('remove-todo', todo.id)">
            &times;
        </button>
    </li>
</template>

<script>
export default {
    props: {
        todo: {
            type: Object,
            required: true
        },
        index: Number
    },
    filters: {
        uppercase(value) {
            return value[0].toUpperCase() + value.slice(1);
        }
    }
}
</script>

<style scoped>
    li {
        
        border: 2px solid black;
        display: flex;
        justify-content: space-between;
        padding: .5rem 2rem;
        padding-left: 1rem;
        margin-bottom: 1rem;
        
    }
    input {
        width: 30px;
        height: 30px;
        margin-right: 1rem;
    }
    button {
        width: 35px;
    }
    .rm {
        background: #333333;
        color: white;
        border-radius: 30%;
        font-size: 1.5rem;
    }
    
    .done {
        text-decoration: line-through;
    }
</style>