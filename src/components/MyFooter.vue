<template>
    <div class="todo-footer" v-show="total">
          <label>
            <!-- 第一种方式写全选or取消全选，使用:checked="isAll" @change -->
            <!-- <input type="checkbox" :checked="isAll" @change="checkAll"/> -->
            <!-- 第二种方式写，使用v-model，但是需要把计算属性写成完整的getter and setter -->
            <input type="checkbox" v-model="isAll"/>
          </label>
          <span>
            <span>已完成{{doneTotal}}</span> / 全部{{total}}
          </span>
          <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
        </div>
</template>

<script>
export default {
    name: 'MyFooter',
    props: ['todos', 'checkAllTodo', 'clearAllTodo'],
    computed: {
      total(){
        return this.todos.length
      },
      doneTotal(){
          return this.todos.reduce((pre, current) => {
              // console.log(pre)
              return pre + (current.done ? 1 : 0)
          },0)
      },
      isAll:{
        get(){
          return this.doneTotal === this.total && this.total > 0
        },
        set(value){
          this.checkAllTodo(value)
        }
      },
    },
    
    methods: {
      // 这个方法就是为了配合第一种方法全选
      // checkAll(e){
      //   this.checkAllTodo(e.target.checked)
      // },
      clearAll(){
        this.clearAllTodo()
      }
    },
}
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