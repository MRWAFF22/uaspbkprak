<template>
    <div class="stopwatch-widget">
      <h2>StopWatch</h2>
      <p>{{ formatTime }}</p>
      <div>
        <button @click="startStopwatch" :disabled="isRunning">Start</button>
        <button @click="stopStopwatch" :disabled="!isRunning">Stop</button>
        <button @click="resetStopwatch">Reset</button>
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
    background-color:  cornflowerblue;
    border: 1px solid #ccc;
    padding: 50px;
    margin-bottom: 20px;
  }
  
  .stopwatch-widget h2 {
    color: white;
    font-size: 24px;
    margin-bottom: 10px;
  }
  
  .stopwatch-widget p {
    color: white;
    font-size: 18px;
    margin-bottom: 10px;
  }
  
  .stopwatch-widget button {
    padding: 10px 20px;
    background-color: lightblue;
    color: white;
    border: none;
    border-radius: 4px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .stopwatch-widget button:hover {
    background-color: blue;
  }
  
  .stopwatch-widget button:disabled {
    background-color: lightblue;
    color: whitesmoke;
    cursor: not-allowed;
  }
  </style>