<template>
  <div class="main">
    <div class="header">
      <h2>Vue To Do List</h2>
      <p>Simple Todo list with adding and filter by diff status</p>
    </div>
    <div class="center">
      <div class="addToDoList">
        <input type="text" v-model="todoItem" placeholder="add to do item"
               @keyup.enter="enterAddToDoItem(todoItem)"
               style="width: 80%;"></input>
        <Button @click="addToDoItem(todoItem)">add</Button>
      </div>
      <div class="todolist">
        <ul class="listView" v-show="todoList.length">
          <li v-for="item in generateFilterList">
            <div class="todoitem">
              <input type="checkbox" v-model="item.isComplete"/>
              <label v-show="!item.editable"
                     :class="item.isComplete ? 'taskitem' : 'text'">{{item.todoItemName}}</label>
              <input type="text" class="editor" v-model="item.todoItemName"
                     v-show="item.editable"
                     @on-blur="" @on-enter="">
              </input>
            </div>
          </li>
        </ul>
      </div>
      <div class="todoTab">
        <ul class="item-count">
          <li class="action">
            <a :class="{active:visibility='all'}" href="javascript:void(0);" @click="switchTab('ALL')">ALL</a>
          </li>
          <li class="action">
            <a :class="{active:visibility='unCompleted'}"  href="javascript:void(0);"  @click="switchTab('Active')">Active</a>
          </li>
          <li class="action">
            <a :class="{active:visibility='completed'}" href="javascript:void(0);"  @click="switchTab('Complete')">Complete</a>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'TodoList',
    data() {
      return {
        todoList: [],
       // filterList: [],
        todoItem: '',
        tabType:'ALL'
      }
    },
    computed:{
      generateFilterList(){
       if (this.tabType==='ALL'){
         return this.todoList;
       } else if(this.tabType==='Active'){
         return this.todoList.filter((e)=>
         !e.isComplete);
       }else{
         return this.todoList.filter((e)=>{
           e.isComplete;
         })
       }
      }
    },
    methods: {
      enterAddToDoItem(todoItem){
        this.addToDoItem(todoItem);
      },
      addToDoItem(todoItem) {
        if ( todoItem === '') {
          return;
        } else {
          this.todoList.push({
            todoItemName: this.todoItem,
            isComplete: false,
            editable:false
          })
          this.todoItem='';
        }
      },
      switchTab(value){
        this.tabType=value;
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1, h2 {
    font-weight: normal;
  }
 ul{
   list-style-type: none;
 }
  .todoTab ul {
    padding: 0;
    display: inline-block;
    overflow: auto;
  }

 .item-count li {
    display: inline-block;
    margin: 0 10px;
  }

  .main {
    margin: 0 auto;
    width: 80%;
  }
.todoTab{
  text-align: center;
}
  .action{
    float: left;
    list-style: none;
  }
  a {
    border-radius:5px;
    color: #42b983;
    width: 140px;
    height: 30px;
    text-decoration: none;
    text-align: center;
    line-height: 30px;
    display: block;
  }
  .active{
    border:1px solid  #42b983;
  }
</style>
