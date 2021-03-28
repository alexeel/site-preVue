<template>
  <div class="logo">
    <a class="logo__link h3" href="/"
      ><span>A</span><span><span>WESOMEET</span></span></a
    >
  </div>
</template>



<style lang="scss">
.logo {
  &__link {
    display: block;
    &::before {
      content: "<";
      vertical-align: middle;
    }
  }
  span {
    display: inline-block;
    vertical-align: middle;
    transition: 0.4s;
    &:not(:first-child):not(:only-child) {
      position: relative;
      &::before {
        content: "/>";
        position: absolute;
        top: 50%;
        left: 0;
        vertical-align: middle;
        transform: translateY(-50%);
        transition: 0.4s;
      }
      & > span {
        display: block;
        clip-path: polygon(0 0, 0 0, 0 100%, 0% 100%);
      }
    }
  }
  &:hover {
    span {
      &:not(:first-child):not(:only-child) {
        &::before {
          left: 100%;
        }
        span {
          clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
          transition: .4s clip-path .2s, color .4s;
        }
      }
    }
  }
}
</style>
