<template>
    <div class="max-w-lg mx-auto">
        <div class="bg-white shadow-md rounded-lg p-6">
            <h1 class="text-xl font-bold mb-4">Todo List</h1>
            <div class="flex mb-4">
                <div>
                    <input type="text" v-model="newTodo" placeholder="Add a new todo"
                        class="flex-1 border border-gray-300 rounded-md px-4 py-2 mr-2 focus:outline-none focus:border-blue-500"
                        @keyup.enter="addTodo" />
                    <p v-if="errorMessage" class="text-red-800 ">please first enter the todo!</p>
                </div>
                <button @click="addTodo"
                    class="bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600 focus:outline-none focus:bg-blue-600 h-10">
                    Add
                </button>
            </div>
            <ul
                class="flex flex-col gap-3 bg-slate-200 text-gray-700 font bold border border-blue-900 rounded-lg shadow-lg p-4">
                <li v-for="(todo, index) in todos" :key="index"
                    class="flex items-center gap-2 bg-white rounded-sm px-2">
                    <input type="checkbox" v-model="todo.completed">
                    <span :class="{ 'line-through': todo.completed }">{{ todo.text }}</span>
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
            errorMessage: false
        }
    },
    methods: {
        addTodo() {
            if (this.newTodo.trim() === '') {
                this.errorMessage = true;
            } else {
                this.errorMessage = false;
                this.todos.push({ text: this.newTodo, completed: false });
                this.newTodo = "";
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
