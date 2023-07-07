<template>
  <div class="fidget-spinner-widget">
    <h2>Fidget Spinner Game</h2>
    <div class="spinner" :style="`transform: rotate(${rotation}deg)`" @click="spinSpinner">
      <div class="spinner-arm"></div>
    </div>
    <button @click="resetGame">Reset</button>
    <p>{{ status }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      rotation: 0,
      isSpinning: false,
      score: 0,
    };
  },
  computed: {
    status() {
      if (this.isSpinning) {
        return 'Spinning...';
      }
      return `Score: ${this.score}`;
    },
  },
  methods: {
    spinSpinner() {
      if (!this.isSpinning) {
        this.isSpinning = true;
        this.rotation = Math.floor(Math.random() * 360) + 720; // Rotate 2-3 spins (720-1080 degrees)
        setTimeout(() => {
          this.calculateScore();
          this.isSpinning = false;
        }, 2000); // Wait 2 seconds before stopping the spinner
      }
    },
    calculateScore() {
      // Add your own scoring logic here based on the final rotation angle
      this.score = Math.floor(Math.random() * 100) + 1;
    },
    resetGame() {
      this.rotation = 0;
      this.isSpinning = false;
      this.score = 0;
    },
  },
};
</script>

<style scoped>
.fidget-spinner-widget {
  background-color:  cornflowerblue;
  text-align: center;
  padding: 20px;
}

.fidget-spinner-widget h2 {
  color: white;
}

.spinner {
  position: relative;
  width: 150px;
  height: 150px;
  border-radius: 50%;
  border: 5px solid #ccc;
  margin: 0 auto;
  cursor: pointer;
  transition: transform 0.5s;
}

.spinner-arm {
  position: absolute;
  top: 50%;
  left: 0;
  width: 50%;
  height: 5px;
  background-color: #333;
  transform-origin: right center;
  transition: transform 0.5s;
}

button {
  margin-top: 20px;
}

p {
  margin-top: 10px;
}
</style>
