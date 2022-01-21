`
<template>
    <div id="root">
        <div class="todo-container">
            <div class="todo-wrap">
                <MyTop :addTodo="addTodo"></MyTop>
                <MyList :todos="todos" :checkTodo="checkTodo" :removeObj="removeObj"></MyList>

                <!--
                通过父组件给子组件传递函数类型props实现：子给父传递数据-->
                <!--
                通过父组件给子组件自定义绑定事件,子给父传递数据-->
                <MyFooter :todos="todos"
                          :checkAllTodo='checkAllTodo'
                          :clearAllTodo='clearAllTodo'
                          v-on:getStuName="getName"
                          ref="myFooter"></MyFooter>
            </div>
        </div>
    </div>
</template>

<script>
    import MyTop from "./components/MyTop.vue";
    import MyList from "./components/MyList.vue";
    import MyFooter from "./components/MyFooter.vue";

    export default {
        name: "App",
        data() {
            return {
                todos: JSON.parse(localStorage.getItem("todos")) || []
            };
        },
        methods: {
            //获取名称方法
            getName(stuName) {
                console.log('获取到方法名被调用了', stuName)
            },
            /**
             * 定义回调方法
             * @param id
             */
            //勾选或取消勾选todo
            checkTodo(id) {
                this.todos.forEach((todo) => {
                    if (todo.id === id) {
                        todo.done = !todo.done
                    }
                })
            },
            //向todos添加
            addTodo(x) {
                this.todos.unshift(x)
            },
            //删除todo
            removeObj(id) {
                this.todos = this.todos.filter((todo) => {
                    return todo.id !== id
                })
            },
            //全选全不选
            checkAllTodo(done) {
                this.todos.forEach((todo) => {
                    todo.done = done
                })
            },
            //清除所有已经完成的todo
            clearAllTodo() {
                this.todos = this.todos.filter((todo) => {
                    return !todo.done
                })
            }
        },
        components: {
            MyList,
            MyFooter,
            MyTop
        },
        watch: {
            //该种写法是完整的监视器的写法
            todos: {
                //开启深度监视
                deep: true,
                handler(value) {
                    //localStorage运用,往本地storage里面存值
                    localStorage.setItem("todos", JSON.stringify(value))
                }
            }
        },
        mounted() {
            this.$refs.myFooter.$on('getStuName', this.getName)
        }
    };
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
