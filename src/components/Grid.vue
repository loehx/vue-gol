<template>
  <div class="grid">
    <div v-for="(row, y) in rows" class="row" :key="y - rows.length/2">
      <Cell v-for="(cell, x) in row" :key="(y - rows.length/2) + '-' + (x - rows.length/2)" @onMouseMove="onMouseMove(y, x)" :active="cell" />
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'
import Cell from './Cell.vue'

@Component({
  components: {
    Cell
  }
})
export default class Grid extends Vue {
  @Prop({ required: true }) rows!: boolean[][]
  @Prop({ required: true }) cellClicked!: (x: number, y: number) => void
  private clickActive = false

  onMouseMove (y: number, x: number): void {
    if (this.clickActive) this.cellClicked(y, x)
  }

  onMouseDown (e : MouseEvent): void {
    if (e.button === 0) this.clickActive = true
  }

  onMouseUp (e : MouseEvent): void {
    if (e.button === 0) setTimeout(() => { this.clickActive = false }, 1)
  }

  mounted (): void {
    document.addEventListener('mousedown', this.onMouseDown)
    document.addEventListener('mouseup', this.onMouseUp)
  }

  unmount (): void {
    document.removeEventListener('mousedown', this.onMouseDown)
    document.removeEventListener('mouseup', this.onMouseUp)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
.grid {
  background-color: rgb(36, 36, 36);
  display: flex;
  flex-direction: column;
  position: absolute;
  left: 15px;
  right: 15px;
  top: 15px;
  bottom: 15px;
}

.row {
  display: flex;
  flex-basis: 100%;
}
</style>
