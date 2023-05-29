<script setup>
import { ref, nextTick, watch, markRaw } from 'vue';
import { VueFlow, useVueFlow, Panel, MarkerType} from '@vue-flow/core'
import { Background } from '@vue-flow/background'
import { Controls } from '@vue-flow/controls'
import { MiniMap } from '@vue-flow/minimap'
import ComponentPanel from './ComponentPanel.vue'
import Task from './Task.vue'
import Start from './Start.vue'

const { findNode, onConnect, addEdges, addNodes, project, vueFlowRef, setTransform, toObject, updateEdge } = useVueFlow()

const nodeTypes = {
  start: markRaw(Start),
  task: markRaw(Task),
}

const nodes = ref([{
    id: '1',
    type: 'start',
    label: 'start node',
    position: { x: 300, y: 250 },
  }
])
const edges = ref([])

function onEdgeUpdate({ edge, connection }) {
  return updateEdge(edge, connection)
}

let id = 0;
function getId() {
  return `dndnode_${id++}`
}

function onDragOver(event) {
  event.preventDefault()

  if (event.dataTransfer) {
    event.dataTransfer.dropEffect = 'move'
  }
}

onConnect((params) => {
  params.updatable = true;
  params.type = 'smoothstep';
  params.markerEnd = MarkerType.Arrow;
  addEdges(params);
})

function onDrop(event) {
  const type = event.dataTransfer?.getData('application/vueflow')

  const { left, top } = vueFlowRef.value.getBoundingClientRect()
  const position = project({
    x: event.clientX - left,
    y: event.clientY - top,
  })

  const newNode = {
    id: getId(),
    type,
    position,
    label: `New node '${id}`,
  }

  addNodes([newNode])

  // align node position after drop, so it's centered to the mouse
  nextTick(() => {
    const node = findNode(newNode.id)
    const stop = watch(
      () => node.dimensions,
      (dimensions) => {
        if (dimensions.width > 0 && dimensions.height > 0) {
          node.position = { x: node.position.x - node.dimensions.width / 2, y: node.position.y - node.dimensions.height / 2 }
          stop()
        }
      },
      { deep: true, flush: 'post' },
    )
  })
}

</script>
<template>
  <vue-flow 
    :node-types="nodeTypes" 
    :nodes="nodes"  
    :edges="edges" 
    @edge-update="onEdgeUpdate"
    @dragover="onDragOver" 
    @drop="onDrop"
    ref="vueFlowRef"
  >
    <Background />
    <Controls />
    <MiniMap pannable zoomable/>
    <panel>
      <component-panel />
    </panel>
  </vue-flow>
</template>