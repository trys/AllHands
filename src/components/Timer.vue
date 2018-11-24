<template>
  <div class="timer center">
    <h1>{{ timestamp }}</h1>
    <button @click="go" type="button">Go</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      timer: null,
      time: 120
    }
  },

  mounted() {
    this.go();
  },

  beforeDestroy() {
    this.reset()
  },

  props: {
    active: Boolean
  },
  
  watch: {
    active() {
      this.go();
    }
  },

  computed: {
    timestamp() {
      const minutes = Math.floor(this.time / 60);
      const seconds = this.time - minutes * 60;
      const double = d => d <= 9 ? '0' + d : d
      return `${double(minutes)}:${double(seconds)}`
    }
  },

  methods: {
    go() {
      this.reset()
      this.time = 120;
      this.timer = setTimeout(this.update, 2000);
    },

    update() {
      this.time--;
      if (this.time === 0) {
        this.reset();
      } else {
        this.timer = setTimeout(this.update, 1000);
      }
    },

    reset() {
      clearTimeout(this.timer)
    }
  }
}
</script>

<style lang="scss">
  .timer {
    h1 {
      font-size: 25vmin;
    }

    button {
      background: transparent;
      color: inherit;
      font: inherit;
      padding: 0;
      border: none;
      outline: none;
      cursor: inherit;

      &:hover {
        opacity: 0.5;
      }
    }
  }
</style>
