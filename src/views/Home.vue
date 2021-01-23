<template>
  <div class="Home">
    <nav-bar-fillter @filterChange="current = $event" :current="current" />
    <div v-if="projects.length">
      <div v-for="project in filterdProjects" :key="project.id">
       <single-project :project="project"
        @delete="handleDelete"
        @done="handleDone"
        />
      </div>
    </div>   
  </div>
</template>

<script>
import SingleProject from '../components/singleProject.vue'
import NavBarFillter from '../components/navBarFillter.vue'


export default {
  name: 'Home',
  components: {
    SingleProject,
    NavBarFillter
   
  },
  data(){
    return{
      projects:[],
      current:'all'
    }
  },
  mounted(){
    fetch('http://127.0.0.1:3000/projects')
    .then(res => res.json())
    .then(data => this.projects = data )
    .catch(err => console.log(err.message))
  },
  methods:{
    handleDelete(id){
      this.projects = this.projects.filter(project => {
        return project.id !== id
      })
    },
    handleDone(id){
      let p = this.projects.find(project => {
        return project.id === id
      })
      p.complete = !p.complete
    }
  },
  computed:{
    filterdProjects(){
      if(this.current === 'complete'){
        return this.projects.filter(project => project.complete)
      }
      if(this.current === 'ongoing'){
        return this.projects.filter(project => !project.complete)
      }
      return this.projects
    }
  }
}
</script>

<style>
body{
  background: rgb(221, 221, 220);
}
.filter-nav-bar button.active{
  color: rgb(2, 81, 131);
}
</style>
