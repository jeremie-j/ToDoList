<template>
  <div>
    <div id="list">
      <div v-for="task in todoList" :key="task.id">
        <TaskEditing v-if="task.id === taskEdited.id"  :taskEdited="taskEdited" @change="handleTaskChange" @sendUpdate="sendUpdate"></TaskEditing>
        <TaskDone v-else-if="task.done" :task="task" @undone="undone"></TaskDone>
        <DisplayTask v-else :task="task" @toggleUpdate="handleToggleUpdate" @finish="finish" @delete="remove"></DisplayTask>
      </div>
      <h2>Add Task</h2>
      <TaskEditing :taskEdited="taskEdited" @change="handleTaskChange" @sendUpdate="addTask"></TaskEditing>
    </div>
  </div>
</template>

<script>
import TaskEditing from './components/TaskEditing'
import DisplayTask from './components/DisplayTask'
import TaskDone from './components/TaskDone'

export default {
  name: 'App',
  data(){ return{
      taskEdited: {
      },
      todoList:[
      {id:0,title: "Coucou", text: "Pourquoi pas finalement", date: "Jun 21 2021 17:04:42",done:false},
      {id:1,title: "Coucou", text: "Pourquoi pas finalement", date: "Jun 21 2021 17:04:42",done:false},
      {id:2,title: "Coucou", text: "Pourquoi pas finalement", date: "Jun 21 2021 17:04:42",done:false}
      ],
  }},
  components: {
    TaskEditing, DisplayTask,TaskDone
  },
  methods:{
    sendUpdate(){
      let index = this.indexOfTask(this.taskEdited.id)
      this.todoList[index] = this.taskEdited
      this.taskEdited = {}
      },
    remove(arg){
      let id = arg
      let index = this.indexOfTask(id)
      this.todoList.splice(index,1)
    },
    handleToggleUpdate(id){
      let index = this.indexOfTask(id)
      this.taskEdited = { ...this.todoList[index] }
    },
    finish(arg){
      let id = arg
      let index = this.indexOfTask(id)
      this.todoList[index].done = true
    },
    undone(arg){
      let id = arg
      let index = this.indexOfTask(id)
      this.todoList[index].done = false
    },
    indexOfTask(id){
      for(let i =0; i < this.todoList.length;i++){
        if(this.todoList[i].id == id){
          return i
        }
      }
    },
    handleTaskChange(task) {
      this.taskEdited = task
    },
    addTask(){
      let id = this.todoList.length >= 1 ? this.todoList[this.todoList.length - 1].id + 1 : 0
      let title = this.taskEdited.title 
      let text = this.taskEdited.text
      let date = Date().split(' ').splice(1,4).join(' ')
      let done = false
      this.todoList.push({id:id,title: title, text: text, date:date, done:done})
      this.taskEdited = {}
    }
  }
}
</script>

<style src="./css/index.css"></style>