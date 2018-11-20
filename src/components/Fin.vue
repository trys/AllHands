<template>
  <div class="center">
    <h1 class="crest-of-a">👋</h1>
    <a href="https://github.com/trys/AllHands">github.com/trys/AllHands</a>
  </div>
</template>

<style lang="scss">
.crest-of-a {
  animation: 0.5s wave infinite;
  transform: rotate(-20deg);
  transform-origin: 60% 100%;
}

@keyframes wave {
  0% {
    transform: rotate(-20deg);
  }

  50% {
    transform: rotate(20deg);
  }
}
</style>
