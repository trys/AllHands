<template>
  <div>
    <div class="slides" :style="{
      transform: `translateX(-${slide * 200}vw)`
    }" :data-active="slide">
      <Home :active="slide === 0" />
      <Thanks :active="slide === 1" />
      <WeeklyReports />
      <Timer :active="slide === 3" />
      <Dom :active="slide === 4" />
      <Fin />
    </div>
    <button type="button" class="traverse" aria-label="Previous slide" @click="prevSlide" />
    <button type="button" class="traverse" aria-label="Next slide" @click="nextSlide" />
  </div>
</template>

<script>
import Home from './components/Home.vue'
import Thanks from './components/Thanks.vue'
import WeeklyReports from './components/WeeklyReports.vue'
import Timer from './components/Timer.vue'
import Dom from './components/Dom.vue'
import Fin from './components/Fin.vue'

export default {
  name: 'app',

  data () {
    return {
      slide: 0
    }
  },

  mounted () {
    window.addEventListener('keydown', this.keypress);
  },

  beforeDesotry () {
    window.removeEventListener('keydown', this.keypress);
  },

  components: {
    Home,
    Thanks,
    WeeklyReports,
    Timer,
    Dom,
    Fin
  },

  methods: {
    keypress(event) {
      if (event.keyCode === 39) {
          event.preventDefault();
          this.nextSlide();
      } else if (event.keyCode === 37) {
          event.preventDefault();
          this.prevSlide();
      } else if (event.keyCode === 70) {
        if (!document.webkitFullscreenElement) {
            document.documentElement.webkitRequestFullscreen();
        } else {
          if (document.webkitExitFullscreen) {
            document.webkitExitFullscreen(); 
          }
        }
      }
    },

    prevSlide() {
      if (this.slide === 0) return;
      this.slide--;
    },

    nextSlide() {
      if (this.slide === this.$children.length -1) return;
      this.slide++;
    }
  }
}
</script>

<style lang="scss">
html,
body {
  margin: 0;
  padding: 0;
  min-height: 100vh;
  overflow: hidden;
}

html {
  box-sizing: border-box;
  cursor: url('/cursor.png'), pointer;
}

* {
  box-sizing: inherit;
}

a {
  color: inherit;
  text-decoration: none;
}

.slides {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #FFF;
  height: 100vh;
  white-space: nowrap;
  width: 1200vw;
  transition: 1.5s transform cubic-bezier(0.740, 0.070, 0.160, 0.965);
  background: linear-gradient(to right, #212020 0%, #212020 8.333%, #88D3CE 16.666%, #4B1CCF 25%, #09203F 33.333%, #537895 41.666%, #2CD8D5 50%, #537895 58.333%, #F68084 66.666%, #FCCB90 75%, #DF89B5 83.333%, #BFD9FE 100%);

  & > * {
    width: 100vw;
    height: 100vh;
    float: left;
    white-space: normal;

    & + * {
      margin-left: 100vw;
    }
  }
}

h1,
h2 {
  margin: 0;
}

h1 {
  font-size: 10vmin;
}

.center {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.traverse {
  position: fixed;
  height: 15vh;
  width: 50vw;
  bottom: 0;
  left: 0vw;
  background: none;
  border: none;
  outline: none;
  -webkit-tap-highlight-color: transparent;
  z-index: 100;
  cursor: inherit;

  & + .traverse {
    left: 50vw;
  }
}

</style>
