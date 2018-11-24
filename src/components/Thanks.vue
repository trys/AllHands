<template>
  <div class="thanks center">
    <h1><span>#yey</span> <span>#thanks</span></h1>
    <div class="stars">
      <i v-for="({x, y, delay}, i) in numbers" :key="i" :style="{
        left: `${x}vw`,
        top: `${y}vh`,
        animationDelay: `${delay}ms`
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

  methods: {
    rand (min = 0, max = 100) {
      return Math.floor(Math.random() * max) + min
    },

    addNumber () {
      const x = this.rand();
      const y = this.rand();
      const delay = this.rand(100, 2000);
      this.numbers.push({ x, y, delay })
    }
  }
}
</script>

<style scoped lang="scss">
.thanks {
  position: relative;
  
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
  animation: 10s stars linear infinite;
}

@keyframes stars {
  0% {
    transform: translateY(0);
    opacity: 0;
  }

  10%,
  30%,
  50%,
  70%,
  90% {
    opacity: 0;
  }

  20%,
  40%,
  60%,
  80% {
    opacity: 1;
  }

  100% {
    transform: translateY(100px);
    opacity: 0;
  }
}
</style>
