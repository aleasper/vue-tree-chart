<template>
  <div class="task-wrapper">
    <h2>{{task.name}}</h2>
  </div>
</template>

<script>
// {
//             "assigner_id": 19,
//             "due_time": 1630216753,
//             "end_time": 1630209553,
//             "id": 1,
//             "name": "Фикс чего-то там",
//             "owner_id": 13,
//             "priority": 75,
//             "process_name": "Поддержка",
//             "start_time": 1630187953,
//             "started": false,
//             "var_count": 2
//         }
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
  border-radius: 6px;
  background: #ffffff;
  box-shadow: 0 2px 4px 0 #cdcdcd;
  padding: 0.4em 0.6em;
}
.center-text {
  text-align: center;
}
</style>
