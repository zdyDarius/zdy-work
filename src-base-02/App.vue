<template>
<div>
  <h2 v-if="!repname">Loding....</h2>
  <h2 v-else>
    most star repo is
    <a :href="repurl">{{repname}}</a>
  </h2>
</div>
</template>

<script>
import axios from 'axios'
  export default {
   async mounted(){

     try {
       const response= await axios.get('https://api.github.com/search/repositories88?q=vue&sort=stars')
       this.repname=response.data.items[0].name // 得到返回结果数据
       this.repurl=response.data.items[0].html_url
     }catch (e){
      console.log(555)
       alert('网络状态不稳定，请稍后重试')
     }

    },
    data(){
      return {
       repname:'',
       repurl:''
      }
    },

  }
</script>


<style scoped>
  .todo-container {
    width: 600px;
    margin: 0 auto;
  }
  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
</style>
