<script setup>
import { ref, nextTick, watch, markRaw } from 'vue';
import { VueFlow, useVueFlow, Panel, MarkerType} from '@vue-flow/core'

const edges = ref([
  {
    id: 'e1-2',
    type: 'smoothstep',
    updatable: true,
    source: '1',
    target: '2',
    sourceHandle: 'a',
    targetHandle: 'b',
    markerEnd: MarkerType.Arrow,
  },
])
</script>
<template>
  
</template>