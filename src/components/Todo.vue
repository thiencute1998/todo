<template>
    <li>
        <input type="checkbox" v-model="check" @change="updateTodo">
        <span v-if="!edit" @dblclick="editTodo" :class="{check : check}">
            {{title}}
        </span>
        <input v-else type="text" v-model="title" @blur="updateTodo" @keyup.enter="updateTodo" v-focus>
            <span @click="deleteTodo(index)">&times;</span>
    </li>
</template>
<script>
export default {
   props: {
       product: {
           type: Object,
           required: true
       },
       index: {
           type: Number,
           required: true
       },
       checkAll: {
           type: Boolean,
           required: true
       }
   },
   data(){
       return{
           title: this.product.title,
           edit: this.product.edit,
           check: this.product.check,
           beforeEditCache: '',
       }
   },
   watch: {
       checkAll(){
            this.check = this.checkAll;
       }
   },
   methods: {
        deleteTodo(index){
           this.$emit('removeTodo',index);
        },
        editTodo(){
            this.edit = true;
            this.beforeEditCache = this.title;
        },
        updateTodo(){
            if(this.title.trim() == ''){
                this.title = this.beforeEditCache;
            }
            this.edit = false;
            this.$emit('finishedUpdateTodo',{
                'todo': {
                    'title': this.title,
                    'edit': this.edit,
                    'check': this.check
                },
                'index': this.index
            })
        },
   }
}
</script>
<style scoped>
    
</style>