<script setup>
import { ref } from 'vue';
import { Handle, Position } from '@vue-flow/core'
import { NodeToolbar } from '@vue-flow/node-toolbar'

const openCard = ref(false);

function openSettings() {
  openCard.value = true;
  toolbarVisible.value = false;
}
</script>

<template>
  <div 
    class="wrapper"
  >
    <div class="title">Task</div>
    <div class="name">Task name</div>
    <div class="info">other info</div>
  </div>

  <node-toolbar
    :position="Position.Bottom"
    style="display: flex; gap: 0.5rem; align-items: center"
    :is-visible="toolbarVisible"
  >
    <button style="padding: 4px;" @click="openSettings">Settings</button>
    <button style="padding: 4px;">Delete</button>
  </node-toolbar>

  <handle :position="Position.Top" class="handleH"/>
  <handle :position="Position.Right" class="handleH"/>
  <handle :position="Position.Bottom" class="handleH"/>
  <handle :position="Position.Left" class="handleH"/>
  <!-- this is for testing
  <div v-if="openCard">this is config</div>
   -->
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
.handleH {
  background-color: #979797;
}
</style>