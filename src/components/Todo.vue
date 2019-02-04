<template>
    <div class="row">
        <div class="col">
            <input
                    class="form-control"
                    v-model="todo_text"
                    type="text"
                    @keydown.enter="addTodo"
                    placeholder="Enter todo .."
            >

            <br>

            <ul class="list-group list-group-flush"
                v-if="todo_list.length">
                <TodoItem
                        v-for="todo in todo_list"
                        :key="todo.id"
                        :todo="todo"
                        @remove="removeTodo"
                />
            </ul>

            <code v-else class="text-center">
                No todo list
            </code>
        </div>
        <div class="col">
            <!--<div class="jumbotron">-->
            <!--{{log_message}}-->
            <!--</div>-->
            <div class="card bg-light">
                <div class="card-body">
                    <pre>{{log_message}}</pre>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import TodoItem from "./TodoItem";

    let todo_id = 1;
    export default {
        name: 'Todo',
        components: {TodoItem},
        props: {
            value: {
                type: String,
                default: '',
            }
        },
        data() {
            return {
                log_message: "",
                todo_text: "",
                todo_list: [
                    {id: todo_id++, text: `Todo ${todo_id}`},
                    {id: todo_id++, text: `Todo ${todo_id}`},
                    {id: todo_id++, text: `Todo ${todo_id}`},
                    {id: todo_id++, text: `Todo ${todo_id}`},
                    {id: todo_id++, text: `Todo ${todo_id}`},
                ]
            }
        },
        methods: {
            addTodo() {
                const todoText = this.todo_text.trim();
                if (todoText) {
                    this.todo_list.push({
                        id: todo_id++,
                        text: todoText,
                    });
                    this.addToLog(`${todoText} added`)
                }
                this.todo_text = ''
            },
            removeTodo(idToRemove) {
                console.log(idToRemove);
                if (idToRemove) {
                    this.todo_list = this.todo_list.filter(todo => {
                        if (todo.id === idToRemove) {
                            this.addToLog(`${todo.text} removed`)
                        }
                        return todo.id !== idToRemove;
                    })

                }
            },
            addToLog(message) {
                if (message) {
                    const time = new Date().toLocaleString();
                    this.log_message += `[${time}] ${message} \n`;
                }
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .card-body > pre {
        font-size: .8rem;
        color: gray;
        font-family: 'Consolas', 'Deja Vu Sans Mono', 'Bitstream Vera Sans Mono', monospace;
    }
</style>
