<template>
  <div class="gol">
    <div class="grid-wrapper">
      <Grid :rows="rows" :cellClicked="cellClicked" />
    </div>
    <ControlBar
      :running="running"
      :size="size"
      :fps="fps"
      @start="start"
      @stop="stop"
      @run="run"
      @clear="clear"
      @shuffle="shuffle"
      @resize="resize"
      @setFps="setFps"
      @loadPattern="loadPattern"
  />
  </div>
</template>

<script lang="ts">
import { Component, Vue, Watch } from 'vue-property-decorator'
import { generateGrid, activateCell, doLifecycle, randomSpawn, loadPattern } from './core'
import Grid from './Grid.vue'
import ControlBar from './ControlBar.vue'

@Component({
  components: {
    Grid,
    ControlBar
  }
})
export default class GameOfLife extends Vue {
  rows = generateGrid(50)
  running = false
  size = 50
  fps = 5
  intervalId = 0

  cellClicked (y: number, x: number): void {
    console.log(y, x)
    this.rows = activateCell(this.rows, x, y)
  }

  start (): void {
    this.intervalId = setInterval(() => this.run(), 1000 / this.fps)
    this.running = true
  }

  stop (): void {
    if (this.intervalId) clearInterval(this.intervalId)
    this.running = false
  }

  run (): void {
    this.rows = doLifecycle(this.rows)
  }

  clear (): void {
    this.rows = generateGrid(this.size)
  }

  shuffle (): void {
    console.log('shuffle')
    this.rows = randomSpawn(this.rows)
  }

  resize (size: number): void {
    this.size = size
  }

  setFps (fps: number): void {
    this.fps = fps
    this.stop()
    this.start()
  }

  async loadPattern (patternName: string): Promise<void> {
    this.rows = await loadPattern(patternName, 30, this.rows)
  }

  @Watch('size')
  sizeChanged (size: number): void {
    this.rows = generateGrid(size, this.rows)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
.grid-wrapper {
  padding-bottom: 100%;
  position: relative;
}
</style>
