<template>
    <form @submit.prevent="onSubmit">
        <input type="text" v-model="title">
        <button type='submit'>Create</button>
    </form>
</template>

<script>
export default {
    data() {
        return {
            title: ''
        }
    },
    methods: {
        onSubmit() {
            if (this.title.trim()) {
                const newTodo = {
                    id: Date.now(),
                    title: this.title,
                    completed : false,
                }
                this.$emit('add-todo', newTodo)
                this.title =''
            }
        }
    }
}
</script>

<style scoped>
    form {
        margin: 0 auto;
        display: flex;
        max-width: 400px;
        margin-bottom: 20px;
    }
    input { 
        width: 80%;
        height: 30px;
    }
    button{
        width: 20%;
        height: 36px;
    }
</style>