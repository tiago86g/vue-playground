<template>
  <div id="calculator">
    <CalculatorContainer/>
  </div>
</template>

<script lang="ts">
import CalculatorContainer from '../components/CalculatorContainer.vue';

export default {
  name: 'Calculator',
  components: {
    CalculatorContainer,
  },
};
</script>
