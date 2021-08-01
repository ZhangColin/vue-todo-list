<template>
  <ul class="todo-main">
    <!-- <transition-group name="todo" appear> -->
    <transition-group
      name="animate__animated animate_bounce"
      appear
      enter-active-class="animate__swing"
      leave-active-class="animate__fadeOutDown"
    >
      <todo-item v-for="todo in todos" :key="todo.id" :todo="todo" />
    </transition-group>
  </ul>
</template>

<script>
import "animate.css";
import TodoItem from "./TodoItem.vue";
export default {
  name: "TodoList",
  components: { TodoItem },
  props: ["todos"],
};
</script>

<style scoped>
/*main*/
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}

.todo-enter-active {
  animation: todoAnimate 0.5s linear reverse;
}

.todo-leave-active {
  animation: todoAnimate 0.5s linear;
}

@keyframes todoAnimate {
  from {
    transform: translateX(0px);
  }
  to {
    transform: translateX(100%);
  }
}
</style>