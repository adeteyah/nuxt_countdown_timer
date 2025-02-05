<script>
export default {
  data() {
    return {
      seconds: 0,
      isPaused: false,
    };
  },
  methods: {
    reset() {
      this.seconds = 0;
    },
    increment(n) {
      this.seconds = this.seconds + n;
    },
    printCountdown(n) {
      let hours = Math.floor(n / 3600);
      let minutes = Math.floor((n - hours * 3600) / 60);
      let seconds = n - hours * 3600 - minutes * 60;
      return hours + ":" + minutes + ":" + seconds;
    },
    startCountdown() {
      this.isPaused = false;
      this.thisCountdown = setInterval(() => {
        if (this.seconds > 0 && this.isPaused == false) {
          this.seconds--;
        } else {
          clearInterval(this.thisCountdown);
        }
      }, 1000);
    },
    pauseCountdown() {
      this.isPaused = true;
    },
  },
};
</script>

<template>
  <div class="h-svh flex gap-4 justify-center items-center">
    <div>{{ printCountdown(seconds) }}</div>
    <input type="text" v-model="seconds" />
    <button v-on:click="increment(15)">+0:15</button>
    <button v-on:click="increment(30)">+0:30</button>
    <button v-on:click="increment(60)">+1:00</button>
    <button v-on:click="increment(300)">+5:00</button>
    <button v-on:click="startCountdown()">Start</button>
    <button v-on:click="pauseCountdown()">Pause</button>
    <button v-on:click="reset()">Reset</button>
  </div>
</template>
