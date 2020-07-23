<template>
  <div>
    {{ msg }}
    <form>
      <button type="button" @click="addTodo()">タスクを追加</button>
      <button type="button" @click="removeTodo()">終了したタスクを削除</button>
      <p>
        タスクを入力：
        <input type="text" v-model="newTodo" />
      </p>
      <p>タスク: {{ newTodo }}</p>
    </form>
    <div class="task-list">
      <label class="task-list__item" v-for="todo in todos" :key="todo.text">
        <input type="checkbox" v-model="todo.done" />
        <input type="checkbox" v-model="todo.editing" />
        <input v-if="todo.editing" v-model="todo.text" @keyup.enter="todo.editing = !todo.editing" />
        <span v-else>{{ todo.text }}</span>
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data: () => {
    return {
      todos: [
        {
          text: "vue-router",
          done: false,
          editing: false,
        },
        {
          text: "vuex",
          done: false,
          editing: false,
        },
        {
          text: "vue-loader",
          done: false,
          editing: false,
        },
        {
          text: "awesome-vue",
          done: true,
          editing: false,
        },
      ],
      newTodo: "",
    };
  },
  methods: {
    // eslint-disable-next-line no-unused-vars
    addTodo: function (event) {
      let text = this.newTodo && this.newTodo.trim();
      if (text.length === 0) {
        return;
      }
      this.todos.push({
        text: text,
        done: false,
        editing: false,
      });
      this.newTodo = "";
    },
    // eslint-disable-next-line no-unused-vars
    removeTodo: function (event) {
      for (let i = this.todos.length - 1; i >= 0; i--) {
        if (this.todos[i].done) {
          this.todos.splice(i, 1);
        }
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@mixin flex-vender() {
  display: flex;
  display: -webkit-flex;
  display: -moz-flex;
  display: -ms-flex;
  display: -o-flex;
}

.task-list {
  @include flex-vender;
  flex-direction: column;
  align-items: center;
  &__item {
    width: 270px;
    text-align: left;
    $element: #{&};
    &--checked {
      @extend #{$element};
      color: #85a6c6;
    }
  }
}
</style>
