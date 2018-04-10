<template>
  <b-container class="bv-example-row">
    <b-row align-h="center">
      <b-col class="counter" cols="4">
        {{ formattedTime }}
      </b-col>
    </b-row>
    <b-row align-h="center">
      <b-col cols="12">
        <b-button size="lg" :variant="modeClass" @click="toggle">{{ cta }}</b-button>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
const START_LABEL = 'Start';
const STOP_LABEL = 'Stop';

export default {
  name: 'timer',
  props: {
    duration: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      interval: null,
      seconds: 0,
    };
  },
  computed: {
    formattedTime() {
      const second = this.seconds % 60;
      const minute = Math.floor(this.seconds / 60);

      const textSecond = `${second}`.padStart(2, '0');
      const textMinute = `${minute}`.padStart(2, '0');

      return `${textMinute}:${textSecond}`;
    },
    cta() {
      if (this.interval === null) {
        return START_LABEL;
      }
      return STOP_LABEL;
    },
    modeClass() {
      return this.interval === null ? 'success' : 'danger';
    },
  },
  created() {
    this.reset();
  },
  methods: {
    reset() {
      this.seconds = this.duration;
    },
    start() {
      this.interval = setInterval(() => {
        this.seconds -= 1;
        if (this.seconds <= 0) {
          this.stop();
          this.reset();
        }
      }, 1000);
    },
    stop() {
      clearInterval(this.interval);
      this.interval = null;
    },
    toggle() {
      if (this.interval === null) {
        this.start();
      } else {
        this.stop();
      }
    },
  },
};
</script>

<style>
.counter {
  font-size: 8rem;
}
</style>
