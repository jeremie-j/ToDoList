<template>
  <div class="task">
    <div class="header">
      <input
        type="text"
        :value="taskEdited.title"
        @input="handleChange('title', $event.target.value)"
        class="taskTitle"
      />
      <p class="date">{{ taskEdited.date }}</p>
    </div>
    <textarea cols="30" rows="10" :value="taskEdited.text" @input="handleChange('text', $event.target.value)"></textarea>
    <div class="button-wrapper">
      <button @click="$emit('newTask')">Add</button>
    </div>
  </div>
</template>

<script>
export default {
  methods:{
      addTask(){
          let date = Date().split(' ').splice(1,4).join(' ')
          let newTask = {title: this.newTaskTitle, text: this.newTaskText, date:date, done:false, editing:false}
          this.newTaskTitle = ''
          this.newTaskText = ''
          console.log(newTask)
        //   taskList.todoList.push(newTask)
      }
  }
};
</script>
