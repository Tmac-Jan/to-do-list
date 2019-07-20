<template>
  <div class="main">
    <div class="header">
      <h2>Vue To Do List</h2>
      <p>Simple Todo list with adding and filter by diff status</p>
    </div>
    <div class="center">
      <div class="addToDoList">
        <input type="text" v-model="todo" placeholder="add to do item" style="width: 90%;"></input>
        <Button >add</Button>
      </div>
      <div class="todolist">
        <ul class="listview" v-show="todoList.length">
          <li v-for="item in filterList">
            <div class="todoitem">
              <input type="checkbox" v-model="item.isComplete"/>
              <label v-show="!item.editable"
                     :class="item.isComplete ? 'taskitem' : 'text'">{{item.title}}</label>
              <input type="text" class="editor" v-model="item.title"
                     v-show="item.editable"
                     @on-blur="" @on-enter="">
              </input>
            </div>
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
        todoList:[],
        filterList:[]
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1, h2 {
    font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }
.main{
  margin: 0 auto;
  width: 80%;
}
  a {
    color: #42b983;
  }
</style>
