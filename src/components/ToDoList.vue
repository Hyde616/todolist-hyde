<script setup lang="ts">
import { ref, computed} from 'vue'

interface Item {
  task: string
  isActive: boolean
}

const tasks = ref<Item[]>([])

const completedTasks = computed(() => tasks.value.filter((item) => item.isActive == true))
const notCompletedTasks = computed(() => tasks.value.filter((item) => item.isActive != true))

const newTaskName = ref('')

const addItem = () => {
    if(!(newTaskName.value=='')){
        tasks.value.push({ task: newTaskName.value , isActive: false})
        newTaskName.value=''
    }
    
}

const moveTask = (itemName: Item) => {
  itemName.isActive = !itemName.isActive
}

</script>

<template>
    <div>
        <h1>ToDoList</h1>
        <h2>未完了タスク</h2>
    </div>
    <ul v-for="item in notCompletedTasks" :key="item.task" >
        <li>
          <div>{{ item.task }} </div>
          <div><button @click="moveTask(item)">完了</button></div>
        </li>
      </ul>
    <div>
        <h2>完了タスク</h2>
    </div>
    <ul>
        <li v-for="item in completedTasks" :key="item.task" >
            <div>{{ item.task }} </div>
            <div><button @click="moveTask(item)">戻す</button></div>
        </li>
        
    </ul>
      <div>
        <label>
          新規タスク名
          <input v-model="newTaskName" type="text" />
        </label>
        <button @click="addItem">追加</button>
      </div>
  </template>
  
  <style>
  </style>
