<template>
  <div>
      <ul>
          <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.item">
              <span v-bind:class="{textCompleted: todoItem.completed}" class="todo-list">{{ todoItem.item }}</span>
              <span v-on:click="removeTodo(todoItem, index)">X</span>
          </li>
      </ul>
      <button class="close-button" v-on:click="clearTodo">전체 삭제</button>
  </div>
</template>

<script>
export default {
    data: function() {
        return {
            todoItems: [],
        }
    },
    methods: {
        removeTodo: function(todoItem, index) {
            localStorage.removeItem(todoItem);
            this.todoItems.splice(index, 1);
        },
        clearTodo: function() {
            localStorage.clear();
            location.reload();
        }
    },
    created: function() {
        if(localStorage.length > 0) {
            for(var i=0; i < localStorage.length; i++) {
                if(localStorage.key(i) !== 'loglevel:webpack-dev-server') {
                    this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
                }
            }
        }
    }
}
</script>

<style scope>
ul {
    position: relative;
    margin: 0 auto;
    border: 1px solid salmon;
    width: 300px;
    margin-top: 50px;
    padding-left: 20px;
    padding-right: 20px;
}
ul li {
    display: flex;
    justify-content: space-between;
    margin: 10px 0;
}
.todo-list {
    display: block;
    width: 200px;
}
.close-button {
    position: absolute;
    left: 50%;
    transform: translate(-50%);
    margin-top: 20px;
}
</style>