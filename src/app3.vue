<script setup>
import { ref , onMounted } from 'vue';

    const name = 'Vue.js';
    const status = ref('bad');
    const tasks = ref(['task1', 'task2', 'task3']);
    const link = 'https://www.google.com';

    const toggleStatus = () => {
      status.value = status.value === 'awesome' ? 'bad' : 'awesome';
    }

    const newTask = ref('');
    const addTask = () => {
      if(newTask.value.trim() !== ''){
        tasks.value.push(newTask.value);
        newTask.value = '';
      }
    }

    const deleteTask = (index) => {
      tasks.value.splice(index, 1);
    }

    onMounted(async()=>{
      try{
        const res = await fetch('https://jsonplaceholder.typicode.com/todos');
        const data = await res.json();
        tasks.value = data.map((task) => task.title);
        console.log(data);
      }catch(err){
        console.log(err);
      }
    })


</script>

<template>
  <div>
    <h1>{{name}}</h1>
    <h2 v-if="status === 'awesome'">Vue.js is awesome</h2>
    <h2 v-else-if="status === 'bad'">Vue.js is not awesome</h2>

    <form @submit.prevent="addTask">
      <input type="text" v-model="newTask">
      <button type="submit">Add Task</button>
    </form>
  <ul>
    <li v-for="(task , index) in tasks" :key="task">
      <span>{{task}} </span>
      <button @click="deleteTask(index)">X</button>
      </li>
  </ul>

  <a :href="link" target="_blank">Google</a>

  <br>
  <button @click="toggleStatus()">Change Status</button>
  </div>

</template>

<style scoped>
h1{
  color: red;
}
</style>


