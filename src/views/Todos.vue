<template>
    <div class="w-[500px] mx-auto">
        <div class="bg-white shadow-md rounded-lg p-6 w-full">
            <h1 class="text-xl font-bold mb-4">Todo List</h1>
            <div class="flex mb-4 justify-between px-2">
                <div>
                    <input type="text" v-model="newTodo" placeholder="Add a new todo"
                        class="flex-1 border border-gray-300 rounded-md px-4 py-2 mr-2 focus:outline-none focus:border-blue-500"
                        @keyup.enter="addTodo" />
                    <!-- <p v-if="error" class="text-red-800 ">please first enter the todo!</p> -->
                </div>
                <button @click="addTodo"
                    class="bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600 focus:outline-none focus:bg-blue-600 h-10">
                    {{this.indextoUpdate !==null? "Update": "Add" }}
                </button>
            </div>
            <ul
                class="flex flex-col gap-3 bg-slate-200 text-gray-700 font bold border border-blue-900 rounded-lg shadow-lg p-4 h-96 overflow-y-auto w-full">
                <li v-for="(todo, index) in todos" :key="index"
                    class="flex items-center gap-2 bg-white rounded-sm p-2 w-full">
                    <input type="checkbox" v-model="todo.completed">
                    <span :class="{ 'line-through': todo.completed }">{{ todo.text }}</span>
                    <div class="flex justify-end items-center w-full gap-2">
                     <button @click="deleteTodo(index)"
                    class="bg-red-500 text-white px-2 py-1 rounded-md hover:bg-red-600 focus:outline-none focus:bg-red-600 ">
                    Delete
                    </button>
                     <button @click="updateTodo(index)"
                    class="bg-gray-500 text-white px-2 py-1 rounded-md hover:bg-gray-600 focus:outline-none focus:bg-gray-600 ">
                Update
                    </button>
                   </div>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            newTodo: '',
            todos: [],
            indextoUpdate: null,
        }
    },
    methods: {
        addTodo() {
            if (this.newTodo.trim() === '') {
                return window.alert("please enter todo before adding")
            } else {
                if (this.indextoUpdate !== null) {
                    this.todos[this.indextoUpdate].text = this.newTodo;
                    this.newTodo=""
                }
                this.todos.push({ text: this.newTodo, completed: false });
                this.newTodo = "";
            }
        },

        deleteTodo(indextodelete) {
            const filteredtodos = this.todos.filter((todo,index)=> index !== indextodelete)
            this.todos = filteredtodos;    
        },

        updateTodo(indextoUpdate) {
            console.log(indextoUpdate)
            if (this.todos[indextoUpdate].completed) {
                return window.alert("to do has been done")
            } else {
                const todoToUpdate = this.todos[indextoUpdate].text;
                this.newTodo = todoToUpdate
                this.indextoUpdate = indextoUpdate;
            }
        }
    }
}
</script>

<style scoped>
.line-through {
    text-decoration: line-through;
}
</style>
