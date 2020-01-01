<template>
  <AppDrop @drop="moveTaskOrColumn" @dragEnter="dragEnter" @dragLeave="dragLeave" ref="drop">
    <AppDrag
      class="task"
      :transferData="{
        type: 'task',
        fromColumnIndex: columnIndex,
        fromTaskIndex: taskIndex
      }"
      @click="goToTask(task)"
    >
      <span class="w-fuill flex-no-shrink font-bold">{{task.name}}</span>
      <p v-if="task.description" class="w-full flex-no-shrink mt-1 text-sm">{{task.description}}</p>
    </AppDrag>
  </AppDrop>
</template>

<script>
import movingTasksAndColumnsMixin from '@/mixins/movingTasksAndColumnsMixin'
import AppDrag from './AppDrag'
import AppDrop from './AppDrop'

export default {
  components: { AppDrag, AppDrop },
  mixins: [movingTasksAndColumnsMixin],
  props: {
    task: {
      type: Object,
      required: true
    },
    taskIndex: {
      type: Number,
      required: true
    }
  },
  methods: {
    goToTask (task) {
      this.$router.push({ name: 'task', params: { id: task.id } })
    },
    dragEnter (e) {
      console.log('DRAG: dragEnter', e.target)
      this.$refs.drop.$el.classList.add('over')
    },
    dragLeave (e) {
      console.log('DRAG: dragleave', e.target)
      this.$refs.drop.$el.classList.remove('over')
    }
  }
}
</script>

<style>
.task {
  @apply flex items-center flex-wrap shadow mb-2 py-2 px-2 rounded bg-white text-grey-darkest no-underline;
}
</style>
