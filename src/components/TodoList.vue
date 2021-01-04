<template>
    <div class="container">
        <input type="text" class="todo-input" v-model="todoField" @keyup.enter="addTodo">
        <h1>Here is the todo list</h1>
        <div>
            <input type="checkbox" :checked="!checkAll" @change="checkAllTodo"> Check All {{!checkAll}}
        </div>
        <ul>
            <Todo v-for="(product,index) in todoFilters" :key="index" :product="product" :index="index" :checkAll="!checkAll" @removeTodo="deleteTodo" @finishedUpdateTodo="updateTodo"> 
                
            </Todo>
        </ul>
        <div class="btn">
            <button :class="{ active : btn == 'all'}" @click="btn = 'all'">All</button>
            <button :class="{ active: btn == 'active'}" @click="btn = 'active'">Active</button>
            <button :class="{ active: btn == 'checked'}" @click="btn = 'checked'">Checked</button>
        </div>
        <div class="clear" v-if="clearChecked">
            <button @click="clearAllChecked">Clear checked</button>
        </div>
        <div class="note">
            <span>
                {{countTodo}} items left
            </span>
        </div>

    </div>      
</template>
<script>

import Todo from './Todo';

export default {
    components:{
        Todo
    },
    data(){
        return{
            todoField: '',
            beforeEditCache: '',
            btn: 'all',
            products: [
                {
                    'title': 'SamSung',
                    'edit': false,
                    'check': false
                },
                {
                    'title': 'Iphone',
                    'edit': false,
                    'check': false
                }
            ],
        }
    },
    computed: {
        countTodo(){
            return this.products.filter(product => !product.check).length;
        },
        checkAll(){
            return this.countTodo != 0;
        },
        clearChecked(){
            return this.products.filter(product => product.check).length > 0;
        },
        todoFilters(){
            if(this.btn == 'all'){
                return this.products;
            }
            else if(this.btn == 'active'){
                return this.products.filter(product => !product.check);
            }
            else if(this.btn == 'checked'){
                return this.products.filter(product => product.check);
            }
            else{
                return this.products;
            }
        }
    },
    // directives: {
    // focus: {
    //     // directive definition
    //     inserted: function (el) {
    //     el.focus()
    //     }
    // }
    // },
    methods: {
        addTodo(){
            if(this.todoField.trim().length){
                this.products.push({
                    'title': this.todoField,
                    'edit': false,
                    'check': false
                });
                this.todoField= '';
            }

        },
        deleteTodo(index){
            this.products.splice(index,1);
        },
        updateTodo(data){
            this.products.splice(data.index,1,data.todo);
        },
        checkAllTodo(event){
            this.products.map(product=> product.check = event.target.checked);
        },
        clearAllChecked(){
            this.products = this.products.filter(product=> !product.check);
        }
    }
}
</script>
<style scoped>

.container{
    max-width: 600px;
    margin: auto;
}
    ul li{
        display: block;
        list-style: none;
        font-size: 24px;
    }
    ul li span{
        cursor: pointer;
    }
    .todo-input{
        display: block;
        width: 60%;
        height: 40px;
        max-width: 400px;
        margin: 0 auto;
        font-size: 24px;
    }
    .check{
        text-decoration: line-through;
    }
    .btn{
        float: left;
    }
    .note{
        float: right;
    }
    .active{
        background: green;
    }
</style>