<template>
  <li>
    <label v-if="!isEdit">
      <input type="checkbox" :checked="todo.done" @change="handleCheck" />
      <span>{{ todo.title }}</span>
    </label>
    <input
      type="text"
      ref="titleTextBox"
      :value="todo.title"
      v-if="isEdit"
      @blur="handleSave($event)"
      @keyup.enter="handleSave($event)"
    />
    <button class="btn btn-danger" @click="handleDelete">删除</button>
    <button class="btn btn-edit" @click="handleEdit" v-if="!isEdit">
      编辑
    </button>
  </li>
</template>

<script>
export default {
  name: "TodoItem",
  data() {
    return {
      isEdit: false,
    };
  },
  props: ["todo"],
  methods: {
    handleCheck() {
      this.$bus.$emit("checkTodo", this.todo.id);
    },
    handleDelete() {
      this.$bus.$emit("removeTodo", this.todo.id);
    },
    handleEdit() {
      this.isEdit = true;
      this.$nextTick(() => {
        this.$refs.titleTextBox.focus();
      });
    },
    handleSave(e) {
      this.isEdit = false;
      // this.$refs.titleTextBox.value
      const newTitle = e.target.value.trim();
      if (newTitle && newTitle !== this.todo.title) {
        this.$bus.$emit("updateTodo", this.todo.id, e.target.value);
      }
    },
  },
};
</script>

<style scoped>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:hover button {
  display: block;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}
</style>