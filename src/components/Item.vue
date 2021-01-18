<template>
    <li 
        @mouseenter='isEnter=true'
        @mouseleave='isEnter=false'
        :class='{active:isEnter}'   
    >
        <label>
            <input 
                type="checkbox" 
                :checked="todo.done" 
                @click='update(index, $event)'
            />
            <span>{{ todo.name }}</span>
        </label>
        <button 
            class="btn btn-danger" 
            :style="{display: isEnter?'block':'none'}"
            @click='deleteT(index)'
        >删除</button>
    </li>
</template>

<script>
export default {
    name: "Item",
    props: ["todo",'index', 'updateTodo','deleteTodo'],
    data(){
        return{
            isEnter:false
        }
    },
    methods:{
        //鼠标覆盖离开 背景颜色更换
        // isEnter(bool){
        //     if(bool) return this.dataisEnter=true;
        //     else return this.dataisEnter=false;
        // }
        update(index, event){
            this.updateTodo(index, event.target.checked)
        },
        deleteT(index){
            if(confirm('确定删除吗?')){
                this.deleteTodo(index);
            }
            
        }
    }
};
</script>

<style scoped>
/*item*/
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
    display: none;
    margin-top: 3px;
}

li:before {
    content: initial;
}

li:last-child {
    border-bottom: none;
}
.active{
    background-color:#ddd;
}
</style>
