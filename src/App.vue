<template>
  <div id="app">
    <PomodoroTimer />
  </div>
</template>

<script setup>
import PomodoroTimer from './components/PomodoroTimer.vue';
</script>

<style>
html, body {
  height: 100%;
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  background-color: black;
  min-height: 100vh;
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
