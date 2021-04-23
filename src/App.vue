<template>
 <p>{{msg}}</p>
 <ul>
  <li v-for="(item,index) in first" :key="index">{{item.name}}</li>
 </ul>
</template>

<script>
 import axios from "axios";
 import { reactive, onMounted,toRefs} from 'vue'
export default {
  name: 'App',
  setup(){
   const state=reactive({
    msg:'这是一个测试daia',
    first:[]

   })
   onMounted(async ()=>{
     let data=await axios.get('/list.json').then(response => {
     return response.data
    }, error => {
     console.log(error);
    });
     state.first=data.first

   })

   return {
    ...toRefs(state)
   }
  }


}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
