<template>
  <div class="home">
    <task-manager></task-manager>
  </div>
</template>

<script>

import TaskManager from '@/components/TaskManager.vue'

export default {
  name: 'home',
  components: {
    TaskManager
  }
}
</script>
