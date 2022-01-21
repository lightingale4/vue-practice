<template>
    <div class="todo-footer" v-show="total">
        <label>
            <input type="checkbox" v-model="isAll"/>
        </label>
        <span>
          <span>已完成{{totalDone}}</span> /全部{{total}}
        </span>
        <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
        <hr>

        <button v-on:click="sendName">获取名字</button>
    </div>
</template>

<script>
    export default {
        name: "MyFooter",
        props: ['todos', 'checkAllTodo', 'clearAllTodo'],
        data() {
            return {
                stuName: 'leo'
            }
        },
        computed: {
            total() {
                return this.todos.length
            },
            totalDone() {
                let count = 0
                //for循环遍历判断
                this.todos.forEach((todo) => {
                    if (todo.done) {
                        count++
                    }
                })
                return count
                //es6中的reduce，类似于java中的lambda表达式
                // return this.todos.reduce((pre, current) => {
                //     console.log(0)
                //     return pre + 1
                // }, 0)
            },
            // isAll() {
            //     return this.total === this.totalDone && this.total > 0
            // },
            isAll: {
                get() {
                    return this.total === this.totalDone && this.total > 0
                },
                set(value) {
                    this.checkAllTodo(value)
                }
            }
        },
        methods: {
            // checkAll(e) {
            //     this.checkAllTodo(e.target.checked)
            // },
            clearAll() {
                this.clearAllTodo()
            },
            sendName() {
                this.$emit('getStuName',this.stuName)
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