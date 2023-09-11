<script setup>
  import { computed } from "vue"

  const props = defineProps({
    todo_list: {
      type: Array,
      required: true,
      default: [],
    },
  })
  const ListCount = computed(() => props.todo_list.length)
  const notExist = computed(() => ListCount.value === 0)
</script>
<template>
  <h3 v-if="notExist">目前無任何TODOLIST</h3>
  <h3 v-else>目前共計 {{ ListCount }} 項 TODOLIST</h3>
</template>