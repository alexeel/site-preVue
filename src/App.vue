<template>
  <div id="app">
    <Header />
    <transition name="slide-fade">
      <router-view />
    </transition>
    <Footer />
  </div>
</template>

<script>
import { TweenMax, TimelineMax } from "gsap";
import Header from "@/components/Header.vue";
import Footer from "@/components/Footer.vue";

export default {
  components: {
    Header,
    Footer,
  },
  mounted() {
    let App = document.querySelector("main");
    let tl = new TimelineMax();
    tl.fromTo(App, 1, { y: 100 }, { y: 0 });
    tl.fromTo(".header", 1, { y: -100 }, { y: 0 });
  },
};
</script>

<style lang="scss">
@import "bootstrap";

$primary-color: #c0ffee;
$secondary-color: #ebac0c;
$dark: #021c1e;
$text: #131313;
$light: #fff;
$grey: #696969;

.slide-fade-enter-active {
  transition: all .6s ease-in;
  transition-delay: .3s;
}
.slide-fade-leave-active {
  transition: all 0.4s ease-out;
}
.slide-fade-enter,
.slide-fade-leave-active {
  opacity: 0;
  padding-top: 3em;
}

@media screen and (min-width: 850px) {
  html {
    &::-webkit-scrollbar {
      width: 0.6em;
    }
    &::-webkit-scrollbar-track {
      background-color: $light;
      box-shadow: inset 0 0 0 0.2em $dark;
    }
    &::-webkit-scrollbar-thumb {
      background-color: $primary-color;
    }
  }
}
body {
  position: relative;
  overflow-x: hidden;
  font-family: "Roboto", sans-serif;
  font-size: 16px;
  background-color: $dark;
  color: $light;
  min-height: 100vh;
}
::-moz-selection {
  background-color: $primary-color;
  color: $dark;
}
::selection {
  background-color: $primary-color;
  color: $dark;
}
main {
  position: relative;
}
h1,
h2,
h3,
h4,
h5,
h6,
.h1,
.h2,
.h3,
.h4,
.h5,
.h6 {
  font-family: "Fira Sans Extra Condensed", sans-serif;
  font-weight: 600;
  text-transform: uppercase;
  margin-bottom: 0.5em;
  &:last-child {
    margin-bottom: 0;
  }
}
h1,
.h1 {
  font-size: 4.6875em;
  line-height: 1.15;
}
h2,
.h2 {
  font-size: 3em;
  line-height: 1.1;
}
h3,
.h3 {
  font-size: 1.875em;
  line-height: 1.2;
}
h4,
.h4 {
  font-size: 1.25em;
  line-height: 1.2;
}
h5,
.h5 {
  font-size: 1.125em;
  line-height: 1.2;
}
h6,
.h6 {
  font-size: 1em;
  line-height: 1.2;
}
p {
  font-size: 1em;
  line-height: 1.6;
  margin-bottom: 1em;
  &:last-child {
    margin-bottom: 0;
  }
}
.lead-text {
  font-size: 1.2em;
}
svg {
  max-width: 100%;
  height: auto;
}
a {
  color: rgba($color: #fff, $alpha: 0.8);
  &:hover {
    color: $primary-color;
    text-decoration: none;
  }
}

.mb {
  margin-bottom: 1.875em;
  &--large {
    margin-bottom: 3.75em;
  }
  &-negative {
    margin-bottom: -1.875em;
    &--large {
      margin-bottom: -3.75em;
    }
  }
}

.bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  right: 0;
  bottom: 0;
  background-size: cover !important;
  background-repeat: no-repeat !important;
  background-position: 50% 50%;
  &-overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    right: 0;
    bottom: 0;
  }
}

.flex-col {
  flex: initial;
  width: auto;
}

ul:not([class]) {
  list-style: none;
  margin-bottom: 1.3em;
  padding-left: 0;
  &:last-child {
    margin-bottom: 0;
  }
  li {
    position: relative;
    padding-left: 1.5em;
    line-height: 1.5;
    margin-left: 0;
    margin-bottom: 0.7em;
    &:last-child {
      margin-bottom: 0;
    }
    &::before {
      content: "\27A4";
      position: absolute;
      top: 0;
      left: 0;
      font-size: 0.8em;
      line-height: 1.9;
    }
  }
}
.button {
  position: relative;
  display: inline-block;
  font-family: "DejaVu Sans Mono", monospace;
  appearance: none;
  cursor: pointer;
  text-align: center;
  padding: 0.6em 1.1em;
  font-size: 1em;
  border: 1px solid;
  margin-bottom: 1em;
  transition: 0.4s ease-in-out;
  & > span {
    position: relative;
    z-index: 9;
  }
  &.primary {
    background: none;
    color: $dark;
    border-color: $primary-color;
    &::before {
      content: "";
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: $primary-color;
      z-index: 1;
      transition: inherit;
    }
    &:hover {
      color: $light;
      &::before {
        width: 0%;
      }
    }
  }
  &.is-outline {
    color: $light;
    border-color: $primary-color;
    &::before {
      width: 0%;
    }
    &:hover {
      color: $dark;
      &::before {
        width: 100%;
      }
    }
  }
  &.disabled {
    cursor: not-allowed;
    color: $light;
    border-color: $grey;
    background-color: $grey;
  }
  &:focus {
    outline: none;
  }
  &:last-child {
    margin-bottom: 0;
  }
}
.section {
  position: relative;
  padding-top: 7.5em;
  padding-bottom: 5.625em;
}

.is-full-height {
  min-height: 100vh;
  height: auto;
  display: flex;
  align-items: center;
}

.table-wrap {
  overflow-x: auto;
}

.divider {
  height: 1px;
  display: block;
  background-color: $grey;
  margin: 1em 0;
  width: 100%;
  &.dark {
    background-color: $light;
  }
  &.primary {
    background-color: $primary-color;
  }
}

@media screen and (min-width: 1921px) {
  :root {
    font-size: 16px;
  }
  body {
    font-size: calc(1rem + 22.4 * (100vw - 120rem) / 4479) !important;
  }
  .container {
    max-width: 77vw;
  }
}
@media screen and (max-width: 1920px) {
}

@media screen and (max-width: 1680px) {
}

@media screen and (max-width: 1540px) {
  h1 {
    font-size: 60px;
  }
  h2 {
    font-size: 42px;
  }
  h3,
  .h3 {
    font-size: 32px;
  }
  .container {
    max-width: 90vw;
  }
}

@media screen and (max-width: 1440px) {
  h1 {
    font-size: 50px;
  }
  h2 {
    font-size: 35px;
  }
  h3,
  .h3 {
    font-size: 27px;
  }
}

@media screen and (max-width: 1366px) {
  h1 {
    font-size: 46px;
  }
  h2 {
    font-size: 33px;
  }
  h3,
  .h3 {
    font-size: 25px;
  }
  h4,
  .h4 {
    font-size: 19px;
  }
  h5,
  .h5 {
    font-size: 17px;
  }
}

@media screen and (max-width: 1280px) {
}

@media screen and (max-width: 1170px) {
}

@media screen and (max-width: 1024px) {
  h1 {
    font-size: 38px;
  }
  h2 {
    font-size: 28px;
  }
  h3,
  .h3 {
    font-size: 22px;
  }
}

@media screen and (max-width: 849px) {
  h1 {
    font-size: 30px;
  }
  h2 {
    font-size: 26px;
  }
  .container {
    max-width: 95vw;
  }
}

@media screen and (max-width: 549px) {
}
</style>
