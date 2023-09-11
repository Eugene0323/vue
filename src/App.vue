<script setup>
import TodoCount from "./components/headers/ListCount.vue"
import TodoItem from "./components/todolists/ListItem.vue"
import { v4 as uuidv4 } from "uuid"
import { ref, reactive, onBeforeMount } from "vue"

const todo_input = ref("")
const todo_list = reactive([])

const addTodo = () => {
  if (todo_input.value !== "") {

    // console.log("addTodo trigger!!")
    const todo = {
      id: uuidv4(),
      title: todo_input.value,
      completed: false,
    }
    todo_list.unshift(todo)
    todo_input.value = ""
  }
}

const removeItem = (id) => {
  const index = todo_list.findIndex((todo) => {
    return todo.id === id
  })

  todo_list.splice(index, 1)
  // save(StorageKey, devices)
}
</script>

<template>
  <main class="container mx-auto">
    <header class="m-2">
      <h1 class="text-6xl font-thin select-none">TODOLIST</h1>
      <div class="font-semibold select-none text-neutral-600">simple and studid todo app</div>
    </header>
    
    <form class="px-10 py-12 bg-white shadow-sm">
      <section class="flex">
        <input
          type="text"
          placeholder="做點重要的事吧..."
          class="w-full text-2xl focus:outline-none input-lg input input-bordered"
          v-model="todo_input"
        />
        <button @click.prevent="addTodo" class="text-xl btn-lg btn btn-neutral">新增</button>
      </section>
    </form>

    <section class="px-10 py-6 mt-4 bg-white">
      <header>
        <TodoCount :todo_list="todo_list" />
      </header>
      <div>
        <TodoItem @remove-todo-item="removeItem" v-for="todo in todo_list" :todo="todo" />
      </div>
    </section>

    
  </main>
</template>

<style scoped></style>