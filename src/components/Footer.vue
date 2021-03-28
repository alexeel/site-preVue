<template>
  <footer class="footer dark">
    <div class="container">
      <div class="row justify-content-between align-items-center">
        <div class="col flex-col">
          <Logo />
        </div>
        <div class="col flex-col text-right footer-author">
          <a class="footer-author__link" href="/" target="_blank"
            >Desined by -<span>Alex Troshkin</span></a
          >
        </div>
      </div>
    </div>
  </footer>
</template>


<script>
import Logo from "@/components/Logo.vue";

export default {
  components: {
    Logo,
  },
};
</script>


<style lang="scss">
$primary-color: #c0ffee;
$secondary-color: #ebac0c;
$dark: #021c1e;
$text: #131313;
$light: #fff;
$grey: #696969;
.footer {
  position: relative;
  background-color: $dark;
  padding: 1.875em 0;
  z-index: 99;
  &-author {
    &__link {
      span {
        display: block;
        position: relative;
        padding: 0.1em 0.3em;
        &::before {
          content: "";
          position: absolute;
          top: 0;
          left: 0;
          width: 100%;
          height: 100%;
          backdrop-filter: blur(3px);
          transition: backdrop-filter.2s;
        }
      }
      &:hover {
        span {
          &::before {
            backdrop-filter: blur(0px);
          }
        }
      }
    }
  }
}
</style>
