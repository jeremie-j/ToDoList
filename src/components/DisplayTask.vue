<template>
  <div class="task">
    <div class="header">
      <input type="text" v-model="task.title" class="taskTitle" disabled />
      <p class="date">{{ task.date }}</p>
    </div>
    <textarea cols="30" rows="10" v-model="task.text" disabled></textarea>
    <div class="button-wrapper">
      <button @click="$emit('delete', task.id)">Delete</button
      ><button @click="$emit('toggleUpdate', task.id)">Edit</button
      ><button @click="$emit('finish', task.id)">Done</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["task"],
};
</script>
