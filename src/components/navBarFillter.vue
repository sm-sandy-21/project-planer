<template>
  <nav class="filter-nav-bar">
      <button
      @click="updateFillter('all')"
      :class="{ active: current === 'all' }"
      >View All</button>
      <button
       @click="updateFillter('complete')"
       :class="{ active: current === 'complete' }"
      >Completed</button>
      <button
       @click="updateFillter('ongoing')"
       :class="{ active: current === 'ongoing' }"
      >On Going</button>
  </nav>
</template>

<script>
export default {
  props:['current'],
  methods:{
    updateFillter(by){
        this.$emit('filterChange',by)
    }
  }
}
</script>

<style>
.filter-nav-bar button{
  background: none;
  border: none;
  color: #b6b6b8;
  outline: none;
  font-size: 15px;
 
  font-weight: bold;
  cursor: pointer;
}
.filter-nav-bar button.active{
  color: rgb(2, 81, 131);
}

</style>