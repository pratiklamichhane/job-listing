<script>
export default{
  data(){
    return{
      name: 'Vue.js',
      status : 'bad',
      tasks : ['task1', 'task2', 'task3'],
      link : 'https://www.google.com',
    }
  },

  methods:{
    toggleStatus(){
      this.status = this.status === 'awesome' ? 'bad' : 'awesome';
    }
  }
}
</script>

<template>
  <div>
    <h1>{{name}}</h1>
    <h2 v-if="status === 'awesome'">Vue.js is awesome</h2>
    <h2 v-else-if="status === 'bad'">Vue.js is not awesome</h2>

  <ul>
    <li v-for="task in tasks" :key="task">{{task}}</li>
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


