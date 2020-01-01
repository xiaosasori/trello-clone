<template>
  <div @drop.stop="onDrop" @dragover.prevent @dragenter.prevent="dragEnter" @dragleave="dragLeave">
    <slot />
  </div>
</template>

<script>
export default {
  methods: {
    onDrop (e) {
      const transferData = JSON.parse(e.dataTransfer.getData('payload'))
      this.$emit('drop', transferData)
    },
    dragEnter (e) {
      this.$emit('dragEnter', e)
    },
    dragLeave (e) {
      this.$emit('dragLeave', e)
    }
  }
}
</script>
