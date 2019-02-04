<template>
    <li class="list-group-item list-group-item-action  d-flex justify-content-between align-items-center">
        {{todo.text}}
        <span class="badge badge-primary badge-pill"
              @click="$emit('remove', todo.id)">
            &times;
        </span>
    </li>
</template>

<script>
    export default {
        name: "TodoItem",
        props: {
            todo: {
                type: Object,
                required: true
            }
        },
    }
</script>

<style scoped>

</style>