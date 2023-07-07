<template>
  <div class="stopwatch-widget">
    <h2>Stopwatch</h2>
    <div class="timer">
      <p class="timer-display">{{ formatTime }}</p>
    </div>
    <div class="buttons">
      <button class="start-button" @click="startStopwatch" :disabled="isRunning">
        <i class="fas fa-play"></i> Start
      </button>
      <button class="stop-button" @click="stopStopwatch" :disabled="!isRunning">
        <i class="fas fa-stop"></i> Stop
      </button>
      <button class="reset-button" @click="resetStopwatch">
        <i class="fas fa-sync"></i> Reset
      </button>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      isRunning: false,
      startTime: null,
      elapsedTime: 0,
    };
  },
  computed: {
    formatTime() {
      const milliseconds = this.elapsedTime % 1000;
      const seconds = Math.floor(this.elapsedTime / 1000) % 60;
      const minutes = Math.floor(this.elapsedTime / 60000) % 60;
      const hours = Math.floor(this.elapsedTime / 3600000);

      return `${hours}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}:${milliseconds.toString().padStart(3, '0')}`;
    },
  },
  methods: {
    startStopwatch() {
      if (!this.isRunning) {
        this.isRunning = true;
        this.startTime = Date.now();

        this.timerInterval = setInterval(() => {
          this.elapsedTime = Date.now() - this.startTime;
        }, 10);
      }
    },
    stopStopwatch() {
      if (this.isRunning) {
        this.isRunning = false;
        clearInterval(this.timerInterval);
      }
    },
    resetStopwatch() {
      this.isRunning = false;
      clearInterval(this.timerInterval);
      this.elapsedTime = 0;
    },
  },
};
</script>
<style scoped>
.stopwatch-widget {
  border: 2px solid #2c3e50;
  background-color: #f1f1f1;
  padding: 20px;
  margin-bottom: 20px;
  border-radius: 5px;
  text-align: center;
}

.stopwatch-widget h2 {
  color: #2c3e50;
  font-size: 24px;
  margin-bottom: 10px;
}

.timer {
  margin-bottom: 20px;
}

.timer-display {
  color: #333;
  font-size: 48px;
  font-weight: bold;
}

.buttons {
  display: flex;
  justify-content: center;
}

.stopwatch-widget button {
  padding: 10px 20px;
  background-color: #2c3e50;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  margin: 0 10px;
}

.stopwatch-widget button:hover {
  background-color: #ff2121;
}

.stopwatch-widget button:disabled {
  background-color: #ccc;
  color: #999;
  cursor: not-allowed;
}

.stopwatch-widget i {
  margin-right: 5px;
}
</style>