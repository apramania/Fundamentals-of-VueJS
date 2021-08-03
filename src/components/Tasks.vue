<template>
    <div v-for="task in tasks" :key="task.id">
        <Task
         @toggle-task-reminder="$emit('toggle-task-reminder', task.id)"
         @delete-task="$emit('delete-task', task.id)" :data="task" />
    </div>
</template>

<script>
import Task from './Task.vue'
export default {
    name: 'Tasks',
    props: {
        tasks: Array
    },
    components: {
        Task
    },
    emits: ['delete-task', 'toggle-task-reminder']
}
</script>