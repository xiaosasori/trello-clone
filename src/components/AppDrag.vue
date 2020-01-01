<template>
  <div draggable @dragstart.self="onDrag" @dragenter.prevent @dragover.prevent @dragend="dragEnd">
    <slot />
  </div>
</template>

<script>
export default {
  props: {
    transferData: {
      type: Object,
      required: true
    }
  },
  methods: {
    onDrag (e) {
      e.target.style.opacity = '0.5'
      e.dataTransfer.effectAllowed = 'move'
      e.dataTransfer.dropEffect = 'move'
      e.dataTransfer.setData('payload', JSON.stringify(this.transferData))
    },
    dragEnd (e) {
      e.target.style.opacity = '1'
    }
  }
}
</script>

<style>
</style>
