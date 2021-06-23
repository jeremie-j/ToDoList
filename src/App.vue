<template>
<div>
  <taskList></taskList>
  <addTask></addTask>
  </div>
</template>

<script>
import taskList from './components/taskList.vue'
import addTask from './components/addTask.vue'

export default {
  name: 'App',
  components: {
    taskList,
    addTask
  }
}
</script>

<style src="./css/index.css"></style>