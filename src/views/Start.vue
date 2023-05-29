<script setup>
import { Handle, Position } from '@vue-flow/core'
</script>
<template>
  <div class="wrapper">
    <div class="title">Start</div>
    <div class="name">Start Name</div>
    <div class="info">other info</div>
  </div>

  <!-- type="source" doesn't work yet-->
  <handle :position="Position.Top" type="source"/>
  <handle :position="Position.Right" type="source"/>
  <handle :position="Position.Bottom" type="source"/>
  <handle :position="Position.Left" type="source"/>
  
</template>
<style scoped>
.wrapper {
  width: 200px;
  height: 80px;
  background-color: var(--el-color-warning-light-8);
  border-radius: 8px;
  display: flex;
  flex-direction: column;
}
.title {
  height: 20px;
  font-size: 12px;
  font-weight: bold;
  color: var(--el-text-color-regular);
  padding: 4px 8px;
}
.name { 
  height: 40px;
  font-size: 16px;
  font-weight: bold;
  color: var(--el-text-color-primary);
  padding: 4px 8px;
}
.info {
  height: 20px;
  font-size: 12px;
  color: var(--el-text-color-regular);
  padding: 4px 8px;
}
</style>