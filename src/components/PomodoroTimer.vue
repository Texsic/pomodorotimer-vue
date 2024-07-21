<template>
  <div class="main">
    <div class="timer-circle" :style="{ width: size + 'px', height: size + 'px' }">
      {{ formattedTime }}
    </div>

    <div class="control-buttons">
      <button @click="toggleStartPause">
        {{ isRunning ? (isPaused ? 'Resume' : 'Pause') : 'Start' }}
      </button>
      <button @click="resetTimer">Reset</button>
      <button @click="setTimer">Timer</button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const size = ref(200);
const totalSeconds = ref(15 * 60);
const secondsLeft = ref(15 * 60);
const isRunning = ref(false);
const isPaused = ref(false);
let timer = null;

const formattedTime = computed(() => {
  const minutes = Math.floor(secondsLeft.value / 60);
  const seconds = secondsLeft.value % 60;
  return `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
});

const startTimer = () => {
  updateTimer();
  timer = setInterval(updateTimer, 1000);
  isRunning.value = true;
};

const updateTimer = () => {
  if (secondsLeft.value > 0 && !isPaused.value) {
    secondsLeft.value--;
  } else if (secondsLeft.value === 0) {
    clearInterval(timer);
    isRunning.value = false;
    alert('Time is up! Take a break.');
  }
};

const toggleStartPause = () => {
  if (!isRunning.value) {
    startTimer();
  } else {
    isPaused.value = !isPaused.value;
    if (isPaused.value) {
      clearInterval(timer);
    } else {
      startTimer();
    }
  }
};

const resetTimer = () => {
  clearInterval(timer);
  secondsLeft.value = totalSeconds.value;
  isRunning.value = false;
  isPaused.value = false;
};

const setTimer = () => {
  const newTime = prompt('Enter new time in minutes:');
  if (!isNaN(newTime) && newTime > 0) {
    totalSeconds.value = newTime * 60;
    resetTimer();
  } else {
    alert('Invalid input. Please enter a valid number greater than 0.');
  }
};
</script>

<style scoped>
.main {
  background-color: rgb(17, 17, 17);
  border-radius: 15px;
  box-shadow: 0 0 20px rgba(255, 0, 0, 0.809);
  padding: 10px 20px;
  width: 500px;
  height: 400px;
  text-align: center;
  color: black;
  margin: auto;
}

.timer-circle {
  border-radius: 50%;
  margin: 20px auto;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 25px;
  color: crimson;
  border: 8px solid red;
}

.control-buttons {
  margin-top: 75px;
  display: flex;
  justify-content: space-evenly;
}

.control-buttons button {
  background-color: rgb(50, 50, 50);
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
}

.control-buttons button:hover {
  background-color: red;
  transition: background-color 0.3s;
}
</style>
