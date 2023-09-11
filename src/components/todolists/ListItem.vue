<script setup>
import { computed } from "vue"
// import { RouterLink } from "vue-router"

const props = defineProps({
  todo: {
    type: Object,
    required: true,
  },
})

const emits = defineEmits(["remove-todo-item"])
const remove = () => {
  emits("remove-todo-item", props.todo.id)
}
const toggleCompleted = () => {
  props.todo.completed = !props.todo.completed;
}
const url = computed(() => `/devices/${props.todo.id}`)
</script>

<template>
  
  <div class="">
    <input  @change="toggleCompleted" type="checkbox" id="todo_id" class="checkbox" />
    <label for="todo_id" class="text-xl cursor-pointer" :class="{ 'line-through': todo.completed }">
      <RouterLink :to="url">{{ todo.title }}</RouterLink>
    </label>
    <img src = "../../assets/delete.svg" @click = "remove" class="del_icon"/>
  </div>
    
    
  
  
</template>

<style scoped>
.line-through {
  text-decoration: line-through;
}
.del_icon{
  width: 20px;
  max-width: 30px;
  
}
.del_icon:hover{
  transform: scale(2);
}
</style>