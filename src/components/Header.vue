<template>
    <header>
        <h1>{{title}}</h1>
        <Button v-show="homePage" @btn-click="$emit('btn-click')" :text="showAddTask ? 'Close' : 'Add Task'" :color="showAddTask ? 'black' : 'green'" />
    </header>
</template>

<script>
import Button from './Button.vue';

export default {
    name: 'Header',
    props: {
        title: {
            type: String,
            default: "Hello"
        },
        showAddTask: {
            type: Boolean
        }
    },
    components: {
        Button
    },
    computed: {
        homePage(){
            if(this.$route.path == "/"){
                return true
            }else{
                return false
            }
        }
    },
    emits: ['btn-click']
}
</script>

<style scoped>
    header{
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>