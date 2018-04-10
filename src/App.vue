<template>
  <div id="app">
    <Timer :duration='TOMATO_TIME' />
  </div>
</template>

<script>
import Timer from './components/Timer';

const TOMATO_TIME = 25 * 60;

export default {
  name: 'App',
  components: {
    Timer,
  },
  data() {
    return {
      TOMATO_TIME,
    };
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
