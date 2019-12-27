<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <form>
      <button @click="addTodo()">Add Task</button>
      <button @click="removeTodo()">Delete Finished Tasks</button>
      <p>input: <input type="text" v-model="newTodo"></p>
      <p>task: {{ newTodo }}</p>
    </form>
    <div class="task-list">
      <label class="task_list_item"
             v-for="todo in todos"
            :key="todo.id"
            :class="{ 'task_list_item--checked': todo.done }">
        <input type="checkbox" v-model="todo.done">
        <input type="checkbox" v-model="todo.editing">
        <input v-if="todo.editing" v-model="todo.text" @keyup.enter="todo.editing = !todo.editing">
        <span v-else>{{ todo.text }}</span>
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data () {
    return {
      todos: [
        {text: 'vue-router', done: false, editing: false},
        {text: 'vuex', done: false, editing: false},
        {text: 'vue-loader', done: false, editing: false},
        {text: 'awesome-vue', done: true, editing: false},
      ],
      newTodo: "",
    }
  },
  methods: {
    addTodo: function() {
      let text = this.newTodo && this.newTodo.trim()
      if (!text) {
        return
      }
      this.todos.push({
        text: text,
        done: false,
        editing: false,
      })
      this.newTodo = ""
    },
    removeTodo: function() {
      for (let i = this.todos.lentgh - 1; i >= 0; i--) {
        if (this.todos[i].done) this.todos.splice(i, 1)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@mixin flex-vender() {
  display: flex;
  display: -webkit-flex;
  display: -moz-flex;
  display: -ms-flexbox;
  display: -o-flex;
}
.task-list {
  @include flex-vender;
  flex-direction: column;
  align-items: center;
}
.task_list_item {
  width: 270px;
  text-align: left;
  $element: #{&};
  &--checked {
    @extend #{$element};
    color: #85a6c6;
  }
}

</style>
