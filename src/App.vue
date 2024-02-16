
<template>
    <div id="app">
       <h1 class="p-5">Gabbe's Todo App</h1>
       <input type="text" class="p-2
        rounded-lg bg-slate-800 text-purple-900" v-model="newTodo" @keyup.enter="addTodo">
       <button @click="addTodo" class="bg-blue-500 text-white m-5">Add Todo</button>
       <ul>
         <li v-for="(todo, index) in todos" :key="index">
           <div class="flex justify-end">
             <span v-if="editingIndex !== index" @dblclick="startEdit(index)" class="flex items-center text-black">
               {{ todo.text }}</span>
             <input v-else type="text" v-model="todo.text" @blur="finishEdit" @keyup.enter="finishEdit" class="text-black m-5 rounded-lg pl-2">
       
             <button @click="complete(index)" :class="[todo.completed ? 'bg-green-500' : 'bg-blue-500', 'text-white', 'm-3', 'inline-block']">
               {{ todo.completed ? 'Completed' : 'Complete' }}
             </button>
             <button @click="remove(index)" class="bg-red-500 text-white m-3 inline-block">Delete</button>
             <button @click="edit(index)" class="bg-blue-500 text-white m-3 inline-block">Edit</button>
           </div>
         </li>
       </ul>
       <div>{{ remainingCount }} todos left</div>
       <button @click="clearCompleted" class="bg-green-500 text-white m-3">Clear completed todos</button>
     </div>
   
 </template>
 <script>
 export default {
   name: 'App',
   data() {
     return {
       todos: [],
       newTodo: '',
       editingIndex: -1
     };
   },
   computed: {
     remainingCount() {
       return this.todos.filter(todo => !todo.completed).length;
     }
   },
   methods: {
     addTodo() {
       if (this.newTodo.trim() === '') return;
       this.todos.push({ text: this.newTodo, completed: false });
       this.newTodo = '';
     },
     startEdit(index) {
       this.editingIndex = index;
     },
     finishEdit() {
       this.editingIndex = -1;
     },
     complete(index) {
       this.todos[index].completed = true;
     },
     edit(index) {
       this.editingIndex = index;
       this.originalTextValue = this.todos[index].text;
     },
     remove(index) {
       this.todos.splice(index, 1);
     },
     clearCompleted() {
       this.todos = this.todos.filter(todo => !todo.completed);
     }
   }
 };
 </script>
 <style scoped>
 /* styles/tailwind.css */
 @import 'tailwindcss/base';
 @import 'tailwindcss/components';
 @import 'tailwindcss/utilities';
 
 </style>