<template>
  <div>
    <ul>
      <li v-for="(project,i) in projects" :key="i">{{ project.name }}</li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';  
  export default {
    data(){
      return{
        title : 'Hello World',
        apiURL: 'http://localhost:8000/api',
        projects:[],
      }
    },
    methods : {
      getProjects(){
        axios.get(`${this.apiURL}/projects`).then((response)=>{
          console.log(response.data.results);
          this.projects = response.data.results;
        })
      }
    },
    mounted(){
      this.getProjects();
    }
  }
  
</script>

<style lang="scss" scoped>

</style>