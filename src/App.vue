<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <!-- 头部 -->
      <Header
        :addTodo='addTodo'
      />
      <!-- 列表 -->
      <List 
        :todos='todos'
        :updateTodo='updateTodo'
        :deleteTodo='deleteTodo'
      />
      <!-- 底部 -->
      <Footer
        :todos='todos'
        :updateAll='updateAll'
        :deleteAllDone='deleteAllDone'
      />
    </div>
  </div>
</template>

<script>
import Header from './components/Header';
import List from './components/List';
import Footer from './components/Footer';
export default {
  name:'App',
  components:{Header, List, Footer},
  data(){
    return{
      todos:[
      {id:'001', name:'抽烟', done:false},
      {id:'002', name:'喝酒', done:true},
      {id:'003', name:'烫头', done:false},
      {id:'004', name:'代码', done:true}
    ]}
  },
  // updated(){  使用updated搭配本地浏览器本地存储,使数据保存到本地. mounted不行,不更新
  //   localStorage.setItem('todos', JSON.stringify(this.todos))
  // },
  methods:{
    // 新增一个todo
    addTodo(todoObj){
      this.todos.unshift(todoObj);
    },
    // 更新一个todo 用id更新
    // updateTodo(id, done){
    //   console.log(id, done)
    //   this.todos=this.todos.map((todo)=>{
    //     if(todo.id===id) return {...todo, done}
    //     else return todo;
    //   })
    // }
    // 更新一个todo 用index更新
    updateTodo(index,done){
      this.todos[index].done=done;
    },
    //删除一个todo
    deleteTodo(index){
      this.todos.splice(index,1)
    },

    //更新全部todo
    updateAll(done){
      console.log(done)
      this.todos=this.todos.map((todo)=>{
        return {...todo, done}
      })
    },
    deleteAllDone(){
      this.todos=this.todos.filter((todo)=>{
        return !todo.done;
      })
    }


  }
}
</script>

<style>
/*base*/
body {
  background: #fff;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}

.btn:focus {
  outline: none;
}

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