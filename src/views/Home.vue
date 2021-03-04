<template>
  <div class="to-do-list">
    <h2>To Do List</h2>
    <div v-for="toDoList in toDoLists" :key="toDoList.id">     
      <ToDo :toDoList="toDoList" @remove="remove" @done="donetoDoList"></ToDo>
    </div>
  </div>
</template>

<script>
import ToDo from '../components/ToDo.vue'
export default {
  components: {
    ToDo,
    
  },
  data(){
    return {
      toDoLists:[]
    }
  },
  mounted(){
    fetch("http://localhost:3000/toDoLists")
    .then((response)=>{
      return response.json();
    })
    .then((datas)=>{
      this.toDoLists=datas;
    })
    .catch((err)=>{
      console.log(err);
    })
  },
  methods:{
    remove(id){
      this.toDoLists=this.toDoLists.filter(toDoList=>{
        return toDoList.id!=id;
      })
    },
    donetoDoList(id){
      let findtoDoList=this.toDoLists.find(toDoList=>{
        return toDoList.id===id;
      });
      findtoDoList.done=!findtoDoList
    }
  }
}
</script>

<style scoped>
  .to-do-list{
    width: 500px;
    margin: 40px auto;
    
  }
</style>
