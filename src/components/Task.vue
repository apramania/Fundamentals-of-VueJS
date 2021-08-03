<template>
    <div @dblclick="onDoubleClick(data.id)" :class="[data.reminder ? 'reminder' : '', 'task']">
        <h3>
            {{ data.text }}
            <i @click="onDelete(data.id)" class="fas fa-times"></i>
        </h3>
        <p>{{ data.day }}</p>
    </div>
</template>

<script>
export default {
    name: 'Task',
    props:{
        data: Object
    },
    methods:{
        onDelete(id){
            this.$emit('delete-task', id)
        },

        onDoubleClick(id){
            // console.log(id);
            this.$emit('toggle-task-reminder', id)
        }
    }
}
</script>

<style scoped>
.fas{
    color: red;
}
    .task{
        background: #f4f4f4;
        margin: 5px;
        padding: 10px 20px;
        cursor: pointer;
    }

    .task.reminder{
        border-left: 5px solid green;
    }

    .task h3{
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
</style>