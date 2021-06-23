<template>
  <div>
    <div id="list">
      <div v-for="task in todoList" :key="task.id">
        <TaskEditing v-if="task.id === taskEdited.id"  :taskEdited="taskEdited" @change="handleTaskChange" @sendUpdate="sendUpdate"></TaskEditing>
        <TaskDone v-else-if="task.done" :task="task" @undone="undone"></TaskDone>
        <DisplayTask v-else :task="task" @toggleUpdate="handleToggleUpdate" @finish="finish" @delete="remove"></DisplayTask>
      </div>
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
        title: '',
        text: '',
      },
      todoList:[
      {id:0,title: "Coucou", text: "Pourquoi pas finalement", date: "Jun 21 2021 17:04:42",done:false,editing:true},
      {id:1,title: "Coucou", text: "Pourquoi pas finalement", date: "Jun 21 2021 17:04:42",done:false,editing:false},
      {id:2,title: "Coucou", text: "Pourquoi pas finalement", date: "Jun 21 2021 17:04:42",done:false,editing:false}
      ],
  }},
  components: {
    TaskEditing, DisplayTask,TaskDone
  },
  methods:{
    sendUpdate(id){
      let index = this.indexOfTask(id)
      console.log(index)
      this.todoList[index].title = "this.taskEdited.title"
      this.todoList[index].text = "this.taskEdited.text"
      this.todoList[index].editing = false
      },
    remove(arg){
      let id = arg
      console.log(id)
      let index = this.indexOfTask(id)
      this.todoList.splice(index,1)
    },
    handleToggleUpdate(id){
      this.taskEdited = { ...this.todoList[id] }
    },
    finish(arg){
      let id = arg
      let index = this.indexOfTask(id)
      this.todoList[index].done = true
    },undone(arg){
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
    }
  }
}
</script>

<style src="./css/index.css"></style>