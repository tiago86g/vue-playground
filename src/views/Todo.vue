<template>
  <div id="todo">
    <TodoContainer msg="test" />
  </div>
</template>

<script lang="ts">
import TodoContainer from '../components/TodoContainer.vue'

export default {
  name: 'Todo',
  components: {
    TodoContainer,
  },
}
</script>
