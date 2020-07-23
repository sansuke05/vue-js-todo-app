<template>
  <div>
    {{ msg }}
    <form>
      <button>タスクを追加</button>
      <button>終了したタスクを削除</button>
      <p>
        タスクを入力：
        <input type="text" />
      </p>
      <p>タスク:</p>
    </form>
    <div class="task-list">
      <label class="task-list__item" v-for="todo in todos" :key="todo.text">
        <input type="checkbox" />
        <button>編集</button>
        {{ todo.text }}
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
  data() {
    return {
      todos: [
        {
          text: "vue-router",
          done: false,
        },
        {
          text: "vuex",
          done: false,
        },
        {
          text: "vue-loader",
          done: false,
        },
        {
          text: "awesome-vue",
          done: true,
        },
      ],
    };
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
