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
})
</script>

<style scoped>

</style>
