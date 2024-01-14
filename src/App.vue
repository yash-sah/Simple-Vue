<template>
  <div id="app">
    <TaskList />
    <WeatherWidget />
  </div>
</template>

<script>
import TaskList from './views/CustomerDetails.vue';
import WeatherWidget from './views/Customers.vue';

export default {
  components: {
    TaskList,
    WeatherWidget,
  },
};
</script>
