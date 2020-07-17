<template>
  <div id="app">
    <tftMatch/>
  </div>
</template>

<script>
import TftMatch from './components/tftMatch.vue'
export default {
  name: 'App',
  components: {
    TftMatch
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body {
  background: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),
    url("https://images.contentstack.io/v3/assets/blt731acb42bb3d1659/blta164bf600709f56d/5ededb42bfd91c2c81be8b67/TFT_Midset_Launch_Trailer_Banner.jpg?quality=100")
      no-repeat center center fixed !important;
  background-size: cover !important;
}

.bg-tft {
  background: linear-gradient(
    rgba(42, 32, 80, 1),
    rgba(42, 32, 80, 1)
  ) !important;
}
</style>
