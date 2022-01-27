<template>
  <div id="app">
    <GameOfLife />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import GameOfLife from './components/GameOfLife.vue'

@Component({
  components: {
    GameOfLife
  }
})
export default class App extends Vue {}
</script>

<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 75vh;
  margin: 0 auto;
}
</style>
