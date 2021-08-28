<template>
  <div class="task-wrapper">
    {{task}}
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
.task-wrapper {
  width: 100%;
}
</style>
