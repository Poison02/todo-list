<template>
  <div class="todo-header">
        <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keyup.enter="add"/>
    </div> 
</template>

<script>
    //导入 nanoid 帮助生成id
    import {nanoid} from 'nanoid'
    export default {
        name: 'MyHeader',
        props: ['addTodo'],
        data(){
            return {
                //和输入框中的数据进行双向绑定，一个变都变
                title: ''
            }
        },
        methods: {
            add(e){
                // 校验数据
                if(!this.title){
                    return alert("数据输入不能为空！")
                }
                //将用户输入包装成一个todo对象
                const todoObj = {id: nanoid(), title: e.target.value, done: false}
                // console.log(todoObj.title) 
                //通过App中的addTodo函数将新输入的数据传过去
                this.addTodo(todoObj)
                //清空输入框
                this.title = ''
            }
        },
    }
</script>

<style scoped>
    /*header*/
  .todo-header input {
    width: 560px;
    height: 28px;
    font-size: 14px;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 4px 7px;
  }

  .todo-header input:focus {
    outline: none;
    border-color: rgba(82, 168, 236, 0.8);
    box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
  }
</style>