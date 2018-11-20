<template>
  <div class="dom center" :data-active="active">
    <div>
      <img src="/updates.png" alt="Updates from Dom" />
      <img src="/updates-2.png" alt="Updates from Dom" />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    active: Boolean
  },
  
  watch: {
    active() {
      this.go();
    }
  }
}
</script>

<style lang="scss">
.dom > div {
  position: relative;
  width: 60vw;
  height: 80vh;
}

.dom img {
  position: absolute;
  height: 100%;
  width: 100%;
  left: 0;
  top: 0;
  object-fit: contain;

  & + img {
    opacity: 0;
  }
}

[data-active="true"] img {
  animation: 4s fadeOut forwards 2s;

  & + img {
    animation: 4s fadeIn forwards 2s;
  }
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }

  100% {
    opacity: 1;
  }
}

@keyframes fadeOut {
  0% {
    opacity: 1;
  }

  100% {
    opacity: 0;
  }
}

</style>
