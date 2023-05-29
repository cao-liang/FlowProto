<script setup>
function onDragStart(event, nodeType) {
  if (event.dataTransfer) {
    event.dataTransfer.setData('application/vueflow', nodeType)
    event.dataTransfer.effectAllowed = 'move'
  }
}
</script>

<template>
  <div class="panel-layout">
    <div class="start-style" :draggable="true" @dragstart="onDragStart($event, 'start')">Start</div>
    <div class="task-style" :draggable="true" @dragstart="onDragStart($event, 'task')">Task</div>
  </div>
</template>

<style scope>
.panel-layout {
  width: 192px;
  padding: 16px;
  background-color: var(--el-color-info-light-8);
  flex-direction:column;
  gap: 8px;
  display:flex;
}
.panel-layout > div {
  cursor:grab;
}
.start-style {
  width: 160px;
  height: 40px;
  background-color:aquamarine;
  border-radius: 8px;
  padding: 10px 0px;
  text-align: center;
}
.task-style {
  width: 160px;
  height: 40px;
  background-color:rgb(166, 200, 65);
  border-radius: 8px;
  padding: 10px 0px;
  text-align: center;
}
</style>
