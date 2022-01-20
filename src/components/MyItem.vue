<template>
    <li>
        <label>
            <input type="checkbox" :checked="todoObj.done" @change="handleCheck(todoObj.id)"/>
            <!-- 下面方法也能实现，不建议-->
            <!--            <input type="checkbox" v-model="todoObj.done">-->
            <span>{{todoObj.title}}</span>
        </label>
        <button class="btn btn-danger" @click="deleteObj(todoObj.id)">删除</button>
    </li>
</template>

<script>
    export default {
        name: "MyItem",
        methods: {
            handleCheck(id) {
                //通知app组件将done值取反
                this.checkTodo(id)
            },
            deleteObj(id) {
                if (confirm('确定删除吗')) {
                    this.removeObj(id)
                }
            }
        },
        //声明接受todo对象
        props: ['todoObj', 'checkTodo','removeObj']
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

    li:hover {
        background: gray;
    }

    li:hover button {
        display: block;
    }
</style>