<template>
  <div class="inputBox">
      <form>
          <label for="todoInput">할일입력</label>
          <input type="text" id="todoInput" v-model="newTodoItem" v-on:keyup.enter="addTodo">
          <button class="todo-button" v-on:click="addTodo">입력</button>
      </form>
  </div>
</template>

<script>
export default {
    data: function() {
        return {
            newTodoItem: '',
        }
    },
    methods: {
        addTodo: function(e) {
            if(this.newTodoItem !== '') {
                var obj = {completed: false, item: this.newTodoItem};
                localStorage.setItem(this.newTodoItem, JSON.stringify(obj));
                // alert("할 일이 저장되었습니다");
            } else {
                e.preventDefault();
                // alert("할 일을 입력해주세요")
            }
            this.newTodoItem = '';
        }
    }
}
</script>

<style scope>
.inputBox {
    display: flex;
    justify-content: center;
}
form {
    position: relative;
}
form label {
    margin-right: 10px;
}
form label::after {
    content: " :";
}
form input {
    height: 30px;
    width: 300px;
    line-height: 30px;
    padding-left: 10px;
    padding-right:50px;
}
form button {
    margin-left: 10px;
    background-color: #fff;
    border: 2px solid salmon;
    line-height: 30px;
    position:absolute;
    right: 0;
    color: tomato;
    font-weight: bold;
}
</style>