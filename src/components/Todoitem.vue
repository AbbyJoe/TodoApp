<template>
    <div class="todo-item" v-bind:class="{'is-compelete':todo.compeleted}">
        <p>
            <input type="checkbox" v-on:change="markCompelete">
            {{todo.title}}
            <button @click="$emit('del-todo', todo.id)" class="del">x</button>
        </p>
    </div>
</template>

<script>

export default {
    name: 'Todoitem',
    props: ["todo"],
    methods: {
        markCompelete() {
            this.todo.compeleted = !this.todo.compeleted
        }
    }
}
</script>

<style scoped>
     .todo-item {
        background : #f4f4f4;
        padding: 20px;
        border-bottom: 1px #ccc dotted;
        margin-top: 20px;
    }
    .is-compelete {
        text-decoration: line-through;
    }
    .del {
        background: #ff0000;
        color: #fff;
        border: none;
        border-radius: 50%;
        padding: 5px 9px;
        cursor: pointer;
        float: right;
    }
</style>