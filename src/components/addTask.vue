<template>
    <div id="add-task">
            <h2>Add task</h2>
            <div id="add-task">
                <input placeholder="Title" type="text" v-model='newTaskTitle' class="taskTitle">
                <textarea cols="30" rows="10" placeholder="Description" v-model='newTaskText'></textarea>
                <button v-on:click="addTask">Ajouter</button>
            </div>
        </div>
</template>

<script>
export default ({
    methods: {
      addTask(){
          let date = Date().split(' ').splice(1,4).join(' ')
          let newTask = {title: this.newTaskTitle, text: this.newTaskText, date:date, done:false, editing:false}
          this.newTaskTitle = ''
          this.newTaskText = ''
          console.log(newTask)
        //   taskList.todoList.push(newTask)
      }
}
})
</script>

<style scoped>

</style>
