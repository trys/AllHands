<template>
  <div class="thanks center">
    <h1><span>#yey</span> <span>#thanks</span></h1>
    <div class="stars">
      <i v-for="({x, y, visible}, i) in numbers" :key="i" :class={visible} :style="{
        transform: `translate3d(${x}vmin, ${y}vmin, 0)`
      }">✨</i>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      numbers: [],
      cease: false
    }
  },

  mounted () {
    Array.apply(null, Array(20)).forEach(() => {
      this.addNumber()
    })
  },

  props: {
    active: Boolean
  },
  
  watch: {
    active() {
      if (this.active) {
        this.cease = false;
        window.requestAnimationFrame(this.showStar);
      } else {
        this.cease = true;
      }
    }
  },

  beforeDestroy() {
    this.cease = true;
  },

  methods: {
    rand (min = 0, max = 50) {
      return Math.floor(Math.random() * max) + min
    },

    addNumber () {
      const x = Math.round(Math.random()) ? -Math.abs(this.rand()) : this.rand();
      const y = Math.round(Math.random()) ? -Math.abs(this.rand()) : this.rand();
      this.numbers.push({ x, y, visible: Math.round(Math.random()) })
    },

    showStar() {
      if (!this.rand(0, 4)) {
        this.numbers[Math.floor(Math.random() * this.numbers.length) + 0].visible = true;
        this.numbers[Math.floor(Math.random() * this.numbers.length) + 0].visible = false;
      }

      if (!this.cease) {
        window.requestAnimationFrame(this.showStar)
      }
    }
  }
}
</script>

<style scoped lang="scss">
.thanks {
  h1 {    
    span:first-child {
      position: relative;
      left: -3vmin;
      top: -7.5vmin;
    }

    span:last-child {
      position: relative;
      left: 3vmin;
      top: 7.5vmin;

      &:before {
        content: '';
        position: absolute;
        left: -10%;
        bottom: 70%;
        width: 1px;
        height: 10vmin;
        background: #FFF;
        transform: rotate(45deg);
      }
    }
  }
}

.stars i {
  position: absolute;
  font-style: normal;
  opacity: 0;
  transition: 1s opacity;

  &.visible {
    opacity: 1;
  }  
}

@keyframes stars {
  0%,
  100% {
    opacity: 0;
  }

  50% {
    opacity: 1;
  }
}
</style>
