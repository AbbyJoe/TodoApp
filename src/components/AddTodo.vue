<template>
    <div>
        <form @submit="addTodo">
            <input type="text" v-model="title" name="Title" placeholder="Add Todo...">
            <input type="submit" value="Add Todo" class="btn">
        </form>
    </div>
</template>

<script>
export default {
    name: "AddTodo",
    data() {
        return {
            title: ''
        }
    },
    methods: {
        addTodo(e) {
            e.preventDefault();
            const newTodo = {
                title: this.title,
                compeleted: false
            }
            // send to parent
            this.$emit('add-todo', newTodo);
            this.title = ' ';

        }
    }
}
</script>

<style scoped>
    form {
        display: flex;
        margin-top: 20px;
    }
    input[type="text"] {
        flex: 10;
        padding: 10px;
        font-size: 16px;
    }
    input[type="submit"] {
        flex: 2;
        background-color: #5cb85c;
    }
</style>