<template>
    <div id="app" class="container">
        <div class="row">
            <div class="col-10 offset-1">
                <h1 class="text-center">Todo application with Vue</h1>
                <br>
                <Todo/>
            </div>
        </div>
    </div>
</template>

<script>
    import Todo from './components/Todo.vue'

    export default {
        name: 'app',
        components: {
            Todo
        }
    }
</script>

<style>
    @import './style.css';

    body {
        margin-top: 10px;
    }

</style>
