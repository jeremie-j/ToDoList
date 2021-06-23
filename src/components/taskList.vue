<template>
<div id="list">
  <h1>Todo-list</h1>
  <div v-if="todoList.length == 0">
    <h3>No tasks for now.</h3>
    <p>Add your first task rigth under this message:</p>
  </div>
  <div v-else>
    <div
      v-for="task in todoList"
      v-bind:task="task"
      :class="{ 'todo-el': true, finished: task.done }"
      :key="todoList.indexOf(task)"
    >
      <div class="header">
        <input
          v-if="task.editing == false"
          type="text"
          id="title"
          v-model="task.title"
          class="taskTitle"
          :disabled="true"
        />
        <input
          v-else
          type="text"
          id="title"
          v-model="taskEdited.title"
          class="taskTitle"
        />
        <p class="date">{{ task.date }}</p>
      </div>

      <textarea
        v-if="task.editing == false"
        cols="30"
        rows="10"
        :disabled="true"
        v-model="taskEdited.text"
        ></textarea>
        <textarea
        v-else
        cols="30"
        rows="10"
        v-model="taskEdited.text"
        ></textarea>

      <div class="button-wrapper" v-if="task.done">
        <button @click="task.done = false">Mark as not finished</button>
      </div>
      <div class="button-wrapper" v-else>
        <button @click="delTask(task)" v-if="task.editing == false">
          Delete</button
        ><button @click="editTask(task)">Edit</button
        ><button @click="task.editing ? modifyTask(task) : finishTask(task)">
          Done
        </button>
      </div>
    </div>
  </div>
  </div>
</template>

<script scoped>
export default ({
  data(){ return{
      todoList:[
      {title: "Coucou", text: "Pourquoi pas finalement", date: "Jun 21 2021 17:04:42",done:false,editing:false}
      ],
      taskEdited:{
          title: '',
          text: ''
      },
      editing: false
  }},
  methods: {
      addTask(){
          let date = Date().split(' ').splice(1,4).join(' ')
          let newTask = {title: this.newTaskTitle, text: this.newTaskText, date:date, done:false, editing:false}
          this.newTaskTitle = ''
          this.newTaskText = ''
          console.log(newTask)
          this.todoList.push(newTask)
          },
      delTask(task){
          let taskIndex = this.todoList.indexOf(task)
          this.todoList.splice(taskIndex,1)
      },
      editTask(task){
          task.editing = true
          this.taskEdited.title = task.title
          this.taskEdited.text = task.text
      },
      modifyTask(task){
          task.editing = false
          task.title = this.taskEdited.title
          task.text = this.taskEdited.text
      },
      finishTask(task){
          task.done = true
      }
  },
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
