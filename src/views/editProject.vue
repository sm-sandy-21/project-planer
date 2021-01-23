<template>
  <form @submit.prevent="handleUpdate">
      <label>Title</label>
      <input type="text" v-model="title" required>
      <label>Details</label>
      <textarea v-model="details"></textarea>
    <button class="submit">Update Project</button>
  </form>
</template>

<script>
export default {
  props:['id'],
  data(){
    return{
      title:'',
      details:'',
      uri:'http://localhost:3000/projects/' + this.id
    }
  },
  mounted(){
      fetch(this.uri)
      .then(res => res.json())
      .then(data => {
        this.title = data.title
        this.details = data.details
      })
   },
   methods: {
     handleUpdate(){
            let project={
               title: this.title,
               details: this.details
               
            }
         fetch(this.uri,{
             method:'PATCH',
             headers:{'Content-Type' : 'application/json'},
             body: JSON.stringify(project)
         }).then(() => {
             this.$router.push('/')
         }).catch(err => {
             console.log(err)
         })
        }
   }
  
}
</script>

<style>
 form {
        display: block;
        max-width: 420px;
        margin: 10px auto;
        background: rgb(255, 255, 255);
        box-shadow: 1px 2px 5px rgb(59, 59, 59) ;
        text-align: left;
        padding: 40px;
        border-radius: 20px;


    }
    label{
        color: rgb(31, 73, 59);
        display: inline-block;
        margin: 20px 0 10px 0;
        font-size: 14px;
        text-transform: uppercase;
        font-weight: bold;
        letter-spacing: 1px;
    }
    input{    
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;       
        border: 5px solid rgba(240, 233, 233, 0.867);
        border-radius: 10px;           
    }  
   /*   input[type="checkbox"]{
       display: inline-block;
       width: 16px;
       margin: 0 10px 0;
       position: relative;
       top: 2px;

    }*/
    textarea{
        border: 5px solid rgba(240, 233, 233, 0.867);
        width: 100%;
        padding: 10px;
        border-radius: 10px;    
        box-sizing: border-box;
        height: 100px;
    }
    
    form button{
        display: block;
        background: rgb(11, 206, 115);
        margin: 20px auto 0;
        padding: 10px;
        color: white;
        border: 0;
        border-radius: 20px;                  
    }
    /* .submit{
        text-align: center;
    }
    .error{
        color: red;
        margin-top: 20px;
        font-size: 0.8em;
        font-weight: bold;   
    } */
</style>