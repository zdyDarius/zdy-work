<template>
  <li :style="{background:bgcolor}" @mouseenter="handleEnter" @mouseleave="handleEnter">
    <label>
      <input type="checkbox" v-model="todo.complete" />
      <span>{{todo.name}}</span>
    </label>
    <button class="btn btn-danger" v-show="isshow" @click="deleteItem">删除</button>
  </li>
</template>

<script>

  export default {
    props:['todo','index','deletetodo'],
    data () {
      return {
        bgcolor:'white',
        isshow:false
      }
    },
    methods:{
      handleEnter(){

      this.bgcolor=this.isshow?'white':'#cccccc';
      this.isshow=!this.isshow
      },
      deleteItem(){
        if(confirm(`确定删除${this.todo.name}吗?`)){
          this.deletetodo(this.index)
        }

      }
    }
  }
</script>


<style scoped>
  li {
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;
  }

  li label {
    float: left;
    cursor: pointer;
  }

  li label li input {
    vertical-align: middle;
    margin-right: 6px;
    position: relative;
    top: -1px;
  }

  li button {
    float: right;
    margin-top: 3px;
  }

  li:before {
    content: initial;
  }

  li:last-child {
    border-bottom: none;
  }
</style>
