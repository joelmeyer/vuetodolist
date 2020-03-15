<template>
    <div>
        <div v-bind:key="todo.id" v-for="todo in todos">
            <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo',todo.id)"/>
        </div>
    </div>
</template>

<script lang="ts">
import TodoItem from './TodoItem.vue'
import Vue from 'vue'
export default Vue.extend({
  name: 'Todos',
  components: {
    TodoItem
  },
  props: ['todos']
})
</script>
<style lang="stylus" scoped>

</style>
