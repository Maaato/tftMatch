<template>
  <div id="app">
    <tftMatch />
  </div>
</template>

<script>
import TftMatch from "./components/tftMatch.vue";
export default {
  name: "App",
  components: {
    TftMatch,
  },
};
</script>

<style>
@font-face {
  font-family: "roboto_mono";
  src: url("./assets/fonts/robotomono-bold-webfont.woff2") format("woff2"),
    url("./assets/fonts/robotomono-bold-webfont.woff2") format("woff");
}

#app {
  font-family: roboto_mono, helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  font-size: 0.9rem;
}
body {
  background: linear-gradient(rgba(0, 0, 0, 0.1), rgba(0, 0, 0, 0.1)),
    url("./assets/images/tft-set-4-fates-splash.jpg") no-repeat center center
      fixed;
  background-size: cover;
}

.bg-tft {
  background: linear-gradient(rgba(51, 184, 255, 1), rgba(51, 184, 255, 1));
}

li {
  display: inline-block !important;
  margin: 0 10px;
}
</style>
