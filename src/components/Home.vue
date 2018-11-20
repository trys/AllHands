<template>
  <div class="center">
    <div class="letters" @click="start">
      {{ output }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',

  props: {
    active: Boolean
  },
  
  data () {
    return {
      alphabet: 'ABCDEFGHIJLKMNOPQRSTUVWXYZ0123456789',
      letters: 'ABCDEFGHIJLKMNOPQRSTUVWXYZ0123456789',
      words:   'DAISIEALL...HANDS.TUE.27NOV...2018..',
      completed: -1,
      timers: null
    }
  },

  watch: {
    active() {
      if (this.active) {
        this.clear();
        this.completed = 0;
        this.letters = this.alphabet;
        this.timer = setInterval(this.shuffle, 100);
      }
    }
  },

  mounted () {
    this.timer = setInterval(this.shuffle, 100);
  },

  beforeDestroy() {
    this.clear();
  },

  computed: {
    output () {
      return this.letters.split('').join(' ')
    }
  },

  methods: {
    clear() {
      clearInterval(this.timer);
    },

    start() {
      this.completed = 0;
    },

    shuffle () {
      const letters = this.alphabet.split('');
      this.letters = this.letters.split('').map((x, index) => {
        if (index <= this.completed) return this.words[index];
        return letters[Math.floor(Math.random()*letters.length)];
      }).join('')

      if (this.completed !== -1) {
        Math.round(Math.random()) && this.completed++;
      }

      if (this.completed === letters.length) {
        this.clear();
      }
    }
  }
}
</script>

<style scoped lang="scss">
.letters {
  text-align: justify;
  width: 8em;
  font-size: 10vmin;
  letter-spacing: 0.1em;
  font-family: 'Space Mono';
  font-weight: 700;
  
  @supports (-webkit-text-fill-color: transparent) {
    background-image: -webkit-gradient(linear,0% 0%,100% 100%,from(#894739),to(#E7CEA2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
}
</style>
