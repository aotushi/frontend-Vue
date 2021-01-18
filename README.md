## todo-list待办事项列表Vue实现

### 1.静态组件的拆分与实现
#### 1.1 App,Header,List>Item,Footer

### 2.动态组件功能
> 父子组件间通信方式:props+回调函数

#### 2.0 内容动态展示
* List组件使用v-for循环展示<Item/>
#### 2.1 Header组件新增todo项
* 判断输入值是否正确
* 使用回调函数更新父组件中data的todos属性

#### 2.2 Item组件更新
* input标签checkbox输入框更新checked
    ```JavaScript
    - 如何获取checked值?两种方式:
    1.使用动态属性获取 :checked=todo.done
    2.使用数据绑定获取 v-model='变量'

    注意:如果v-model和事件同时存在,是先响应事件再更新v-model的值. 所以在事件回调中打印checked的值还是未更新的.
    - 使用todo的索引index代替id来更新,更简洁
    ```
* 鼠标移入/移出事件:背景颜色出现/消失
    ```JavaScript
    isEnter默认值false
    @mouseenter='isEnter=true'
    @mouseleave='isEnter=false'
    :class="{'active':isEnter}
    ```
* 鼠标移入/移出,button删除按钮显示/消失
* button删除按键事件,更新父组件的todos属性

#### 2.3 Footer组件更新
* 总数量和已完成数量更新
  * 使用computed.获取需要通过计算才有的属性
  ```JavaScript
    - computed中属性可以借用
    - 已完成done使用reduce方法:
    this.todos.reduce((pre, current)=>{
        return pre+=current.done?1:0
    },0)
  ```

* 点击选择框实现全选或全不选

   `event.target.checked`

* 更新选择框, 使用动态属性:checked+computed
    `:checked:countChecked`
    `countChecked(){return this.hasDone===this.allCount && this.allCount > 0}`

* 删除已完成todo

