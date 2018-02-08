<template>
    <div class="todo-list">
        <h1>TODO List</h1>
        <form v-on:submit.prevent="addItem">
            <input type="text" v-model="value">
            <button>Add</button>
        </form>
        <ol>
            <li v-for="(todo, index) in todos" v-bind:class="{ done: todo.isChecked }">
                <p>{{index + 1}}. {{ todo.text }}</p>
                <div class="controls">
                    <button type="button" v-on:click="showChangeForm(index)">Change</button>
                    <button type="button" v-on:click="checkedItem(index)">{{ todo.isChecked ? 'Undone' : 'Done' }}</button>
                    <button type="button" v-on:click="deleteItem(index)">x</button>
                </div>
                <form v-if="todo.isShown" v-on:submit.prevent="changeItem(index)">
                    <input type="text" v-model="todo.text">
                    <button>Ok</button>
                </form>
            </li>
        </ol>
    </div>
</template>

<script>
    export default {
        name: 'ToDo',
        data() {
            return {
                todos: [
                    {
                        text: 'Купить мясо',
                        isChecked: false,
                        isShown: false
                    },
                    {
                        text: 'Посадить дерево',
                        isChecked: false,
                        isShown: false
                    },
                    {
                        text: 'Построить дом',
                        isChecked: false,
                        isShown: false
                    }
                ],
                value: '',
                changingValue: ''
            };
        },
        methods: {
            addItem: function () {
                this.value ? this.todos.push({text: this.value, isChecked: false, isShown: false}) : '';
                this.value = '';
            },
            deleteItem: function (index) {
                this.todos.splice(index, 1);
            },
            checkedItem: function (index) {
                this.todos[index].isChecked = !this.todos[index].isChecked;
                // let done = this.todos.splice(index, 1);
                // this.todos.push(done[0]);
            },
            changeItem: function (index) {
                this.todos[index].isShown = false;
            },
            showChangeForm: function (index) {
                this.todos[index].isShown = true;
            }
        }
    };
</script>

<style>
    .todo-list {
        width: 600px;
        margin: 50px auto;
    }
    ol {
        display: flex;
        flex-direction: column;
        padding: 0;
    }
    ol li {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    .done p {
        color: #ccc;
        text-decoration: line-through;
    }
</style>