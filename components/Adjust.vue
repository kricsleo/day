<script setup lang="ts">
import { onMounted } from 'vue';
import { type Plan, editingPlanId } from '~/composables/days';

const props = defineProps<{
  plan: Plan
  isStart: boolean
}>()

onMounted(() => {
  window.addEventListener('mouseup', () => {
    editingPlanId.value = null
  })
})

function handleMousedown() {
  props.plan.entry = props.isStart ? props.plan.end : props.plan.start
  editingPlanId.value = props.plan.id
}
</script>

<template>
  <button 
    ref="adjustTarget"
    h-full w-1.5 expand-click
    pointer-events-auto cursor-col-resize
    @mousedown.passive="handleMousedown" />
</template>
