<template>
    <ul class="todo-main">
        <MyItem
                v-for="todoObject in todos"
                :key="todoObject.id"
                :todoObj="todoObject"
                :checkTodo="checkTodo"
                :removeObj="removeObj"/>
    </ul>
</template>

<script>
    import MyItem from "./MyItem";

    export default {
        name: "MyList",
        props: ['todos', 'checkTodo', 'removeObj'],
        components: {MyItem},
    };
</script>

<style scoped>
    /*main*/
    .todo-main {
        margin-left: 0px;
        border: 1px solid #ddd;
        border-radius: 2px;
        padding: 0px;
    }

    .todo-empty {
        height: 40px;
        line-height: 40px;
        border: 1px solid #ddd;
        border-radius: 2px;
        padding-left: 5px;
        margin-top: 10px;
    }

</style>