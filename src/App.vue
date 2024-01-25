<template>
  <div id="app" class="bg-light">
    <BMICalculator />
    <CaloricNeedsCalculator />
  </div>
</template>

<script>
import BMICalculator from './components/KalkulatorBMI.vue';
import CaloricNeedsCalculator from './components/KalkulatorZAP.vue';

export default {
  name: 'App',
  components: {
    BMICalculator,
    CaloricNeedsCalculator,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.bg-light {
  background-color: #f8f9fa;
}
</style>
