<template>
    <header class="header">
        <h1>todos</h1>
        <input 
            type="text" 
            class="new-todo" 
            autofocus 
            autocomplete="off" 
            placeholder="What needs to be done?"
            v-model="text"
            @keyup.enter="handleTodo"
        >
    </header>
</template>

<script>
    export default {
        data(){
            return{
                text: ""
            }
        },
        methods: {
            handleTodo() {
                const { text } = this;
                // console.log(keycode)
                // if(keycode === 13 && text !== ""){
                //     this.$emit("insertTodo", text);
                //     this.text="";
                // }
                this.$emit("insertTodo", text);
                this.text="";
                
            }
        }
    }
</script>

<style scoped>
h1 {
  position: absolute;
  top: 0px;
  width: 100%;
  font-size: 100px;
  font-weight: 100;
  text-align: center;
  color: rgba(175, 47, 47, 0.15);
  -webkit-text-rendering: optimizeLegibility;
  -moz-text-rendering: optimizeLegibility;
  text-rendering: optimizeLegibility;
}
</style>