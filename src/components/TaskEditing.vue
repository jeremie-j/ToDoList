<template>
  <div class="task">
    <div class="header">
      <input
        type="text"
        :value="taskEdited.title"
        @input="handleChange('title', $event.target.value)"
        class="taskTitle"
        placeholder="Title"
      />
      <p class="date">{{ taskEdited.date }}</p>
    </div>
    <textarea cols="30" rows="10" placeholder="Description" :value="taskEdited.text" @input="handleChange('text', $event.target.value)"></textarea>
    <div class="button-wrapper" v-once>
      <button @click="$emit('sendUpdate')" v-if="taskEdited.id != undefined">Edit</button>
      <button @click="$emit('sendUpdate')" v-else>Add</button>
    </div>
  </div>
</template>

<script>
export default {
  props:['taskEdited'],
  methods:{
    handleChange(key, value){
      this.$emit('change', { ...this.taskEdited, [key]: value })
    }
  }
};
</script>
