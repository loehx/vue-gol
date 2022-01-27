<template>
  <div
    class="cell"
    :class="{ active }"
    @mousemove="$emit('onMouseMove')"
    @click="$emit('onMouseMove')"
    :style="{ backgroundColor: rgbCode }">
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue, Watch } from 'vue-property-decorator'

@Component
export default class Cell extends Vue {
  @Prop({ required: true }) active!: boolean;
  private activeCounter = 0;
  private rgbCode = '';

  @Watch('active')
  activeChanged (): void {
    this.activeCounter += 10
    this.rgbCode = `rgb(${this.activeCounter - 100},${this.activeCounter - 200},${Math.min(150, this.activeCounter - 0)})`
  }
}
</script>

<style scoped lang="less">
.cell {
  background-color: black;
  margin: 0 0 1px 1px;
  flex-basis: 100%;
}

.active {
  background-color: white !important;
}
</style>
