<template>
<div class="project" :class="{ complete : project.complete }">
    <div class="action">
    <h2 @click="showDetails =!showDetails ">{{ project.title }}</h2>
      <div class="icon">
          <router-link :to="{ name: 'editProject', params:{id:project.id}}">
              <span class="material-icons">edit</span>
          </router-link>       
        <span @click="deleteData" class="material-icons">delete</span>
        <span @click="projectDone" class="material-icons">done</span>
    </div>
    </div>
    <div v-if="showDetails" class="details">
        <p>{{ project.details }}</p>
    </div>
</div>  
</template>

<script>
export default {
    props : ['project'],

    data(){
        return{
        showDetails : false,
        uri : 'http://localhost:3000/projects/'  + this.project.id
        }
    },
    methods: {
         deleteData(){
             fetch(this.uri,{method: 'DELETE'})
             .then(()=>this.$emit('delete',this.project.id))
             .catch(err =>console.log(err))
         },
         projectDone(){
             fetch(this.uri,{
                 method:'PATCH',
                 headers:{'Content-Type' : 'application/json'},
                 body: JSON.stringify({complete : !this.project.complete})
             })
             .then(()=>this.$emit('done',this.project.id))
             .catch(err =>console.log(err))
         } 
    }
}
</script>

<style>
.project{
    margin: 20px 90px;
    background: white;
    padding: 10px 20px;
    border-radius: 20px;
    box-shadow: 1px 2px 5px rgb(59, 59, 59) ;
    border-left: 4px solid #c41306;
    border-right: 4px solid #c41306;
}
h2{
    cursor: pointer;
}
.material-icons{
    font-size: 40px;
    color: rgba(50, 63, 19, 0.61); 
    cursor: pointer;
}
.material-icons:hover{
    color: rgb(125, 211, 130);
}
.project.complete{
     border-left: 4px solid #36ca08;
     border-right: 4px solid #36ca08;
}
</style>