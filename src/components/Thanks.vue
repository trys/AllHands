<template>
  <div class="thanks center">
    <h1><span>#yey</span> <span>#thanks</span></h1>
  </div>
</template>

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
</style>
