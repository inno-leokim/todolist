<template>
    <div id="app">
        <section class="todoapp">
            <Header @insertTodo="insertTodo" />
            <Todo :todos="filteredList" 
                @removeTodo="removeTodo"
                @updateDone="updateDone"
                @updateTodo="updateTodo"
            />
            <Footer 
                :filterType="filterType" 
                :size="filteredList.length"
                @onFilterType="handlefilterType"
            />
        </section>
    </div>
</template>

<script>
import "./assets/css/main.css";

import Header from './components/Header.vue';
import Todo from "./components/Todo.vue";
import Footer from "./components/Footer.vue";

export default {
    data(){
        return {
            todos: [
                {
                    id: new Date(),
                    text: "Vue 테스트하기",
                    isDone: true
                },
                {
                    id: new Date() + 1,
                    text: "spring 테스트하기",
                    isDone: false
                }
            ],
            filterType: 'All'
        }
    },
    components: {
        Header,
        Todo,
        Footer      
    },
    methods: {
        insertTodo(text) {
            this.todos = [
                ...this.todos,
                {
                    id: new Date().getTime(),
                    text,
                    isDone: false
                }
            ]
        },
        removeTodo(id) {
            this.todos = this.todos.filter(todo => todo.id !== id);
        },
        updateDone(id) {
            const todos = [...this.todos];
            const todo = todos.find(todo => todo.id === id);

            if (todo){
                todo.isDone = !todo.isDone;
                this.todos = todos;
            }
        },
        updateTodo({id, text}) {
            const todos = [...this.todos];
            const todo = todos.find(todo => todo.id === id);

            if(todo) {
                todo.text = text;
                this.todos = todos;
            }
        },
        handlefilterType(type) {
            this.filterType = type
        }
    },
    computed: {
        filteredList() {
            switch(this.filterType){
                case 'ALL': {
                    return this.todos;
                }
                case "Active": {
                    return this.todos.filter((todo) => !todo.isDone);
                }
                case "Completed": {
                    return this.todos.filter((todo) => todo.isDone);
                }
                default: {
                    return this.todos;
                }
            }
        }
    }
}
</script>

<style>
</style>
