<script setup>
import DeviceItem from "@/components/devices/Item.vue"
import { v4 as uuidv4 } from "uuid"
import { ref, reactive } from "vue"

const title = "TODO!"
const todo = ref("")
const todolist = reactive([])

const addTodo = () => {
  if (todo !== "") {
    const item = {
      id: uuidv4(),
      title: todo.value,
    }
    todolist.unshift(item)
    todo.value = ""
  }
  
}

const removeItem = (id) => {
  const index = todolist.findIndex((todo) => {
    return todo.id === id
  })

  todolist.splice(index, 1)
  
}


</script>

<template>
      
  <main class="flex flex-col min-h-screen py-8 antialiased bg-slate-50">
    <div class="container mx-auto">
        <header class="m-2">
            <h1 class="text-6xl font-thin select-none">{{ title }}</h1>
            <div class="font-semibold select-none text-neutral-600">simple and studid todo app</div>
        </header>
        <form class="px-10 py-12 bg-white shadow-sm">
        <section class="flex">
            <input type="text" placeholder="做點重要的事吧..." class="input-device" v-model="todo"/>
            <button @click.prevent="addTodo" class="btn-action">新增</button>
        </section>
        </form>
        
        <section>
        <header>
            <DeviceInfo :todolist="todolist" />
        </header>

        <ul>
            <DeviceItem
            @remove-auo-item="removeItem"
            v-for="d in todolist"
            :todo="d"
            />
        </ul>
        </section>
    </div>
  </main>
</template>

<style scoped>
.input-device {
  @apply w-full text-2xl focus:outline-none input-lg input input-bordered;
}


.btn-action {
  @apply text-xl btn-lg btn btn-neutral;
}
</style>
