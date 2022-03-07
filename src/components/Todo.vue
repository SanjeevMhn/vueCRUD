<script>
    export default{
        data(){
            return{
                item: '',
                editItem: '',
                editListItem: false,
                editItemIndex: '',
                todos:[
                    {desc: 'Go on a run', done: true},
                    {desc: 'Buy Groceries', done: false},
                    {desc: 'Clean the kitchen', done: true},
                    {desc: 'Walk the dog', done: false},
                ]
            }
        },
        methods:{
            addItems(item){
                if(!this.editListItem){
                    let check = this.todos.filter((todo)=>{
                        return todo.desc.toLowerCase() === item.toLowerCase();
                    });
                    if(check.length > 0){
                        alert('Item already exists');
                        this.item = '';
                    }else{
                        this.todos.unshift({desc: item, done: false});
                        this.item = '';
                    }
                }else{
                    if(this.item !== ''){
                        this.todos[this.editItemIndex].desc = this.item;
                    }else{
                        alert("Please enter some text");
                    }

                    this.editListItem = !this.editListItem;
                }
            },
            mark(index){
                this.todos[index].done = !this.todos[index].done;
            },
            remove(ind){
                console.log(ind);
                this.todos.splice(ind,1);
            },
            edit(index){ 
                this.item = this.todos[index].desc;
                this.editListItem = !this.editListItem;
                this.editItemIndex = index;
                console.log(this.editItemIndex);
            }
        }
    }
</script>

<template>
    <label for="addItem">Add Item</label>
    <input type="text" name="addItem" id="addItem" v-model="item" @keyup.enter="addItems(item)" >
    <button @click="addItems(item)">Add Item</button>
    <ul class="">
        <li v-for="(todo,index) in todos" :key="index" class="" :class="[todo.done ? 'mark' : '']">
            {{todo.desc}}
            <button @click="mark(index)">Mark</button>
            <button @click="remove(index)">Delete</button>
            <button @click="edit(index)">Edit</button>
        </li>
    </ul>
</template>

<style>
    .mark{
        text-decoration: line-through;
    }
</style>