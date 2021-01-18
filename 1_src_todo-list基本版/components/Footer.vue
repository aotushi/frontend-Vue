<template>
  <div class="todo-footer">
    <label>
      <input 
        type="checkbox" 
        :checked='countChecked'
        @click='checkAll'
      />
    </label>
    <span> <span>已完成{{hasDone}}</span> / 全部{{allCount}} </span>
    <button class="btn btn-danger" @click='deleteAll'>清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "Footer",
  props:['todos', 'updateAll','deleteAllDone'],
  data(){
    return{
      check:null,
      isChecked:''
    }
  },
  methods:{
    deleteAll(){
      if(confirm('确定删除吗?')){
        this.deleteAllDone();
      }
    },
    checkAll(event){
      this.updateAll(event.target.checked)
    }
  },
  computed:{
    hasDone(){
      return this.todos.reduce((preValue, current)=>{return preValue += current.done?1:0},0)
    },
    allCount(){
      return this.todos.length;
    },
    // isAll:{
    //   set(value){
    //     this.updateAll(value);
    //   },
    //   get(){
    //     if(this.hasDone===this.allCount.length && this.allCount>0) return true;
    //     else return false;
    //     //return this.hasDone===this.allCount.length && this.allCount>0;
    //   }
    // }
    countChecked(){
      return this.hasDone===this.allCount && this.allCount>0
    }
  }
};
</script>

<style scoped>
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>
