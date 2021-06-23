<template>
  <div class="task">
    <div class="header">
      <input
        type="text"
        v-model="task.title"
        class="taskTitle"
        disabled
      />
      <p class="date">{{ task.date }}</p>
    </div>
    <div class="button-wrapper">
      <button @click="task.done = false">Mark as not finished</button>
    </div>
  </div>
</template>

<script>
export default {
  props:['task']
};
</script>