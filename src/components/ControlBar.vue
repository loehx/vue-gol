<template>
  <div class="control-bar">
    <div class="panel">
      <button v-show="!running" @click="$emit('start')" title="Start"><font-awesome-icon icon="play" /></button>
      <button v-show="running" @click="$emit('stop')" title="Stop"><font-awesome-icon icon="stop" /></button>
      <button @click="$emit('run')" title="Single lifecycle"><font-awesome-icon icon="forward" /></button>
      <button @click="$emit('clear')" title="Clear"><font-awesome-icon icon="trash" /></button>
      <button @click="$emit('shuffle')" title="Shuffle">
        <font-awesome-icon icon="random" />
      </button>
    </div>

    <div class="panel">
      <PatternLoader @loadPattern="$emit('loadPattern', $event)" />
    </div>

    <div class="panel">
      <button @click="$emit('resize', size + 10)" title="Increase grid size">
        <font-awesome-icon icon="plus" />
      </button>
      {{ size }}x{{ size }}
      <button @click="$emit('resize', size - 10)" title="Decrease grid size">
        <font-awesome-icon icon="minus" />
      </button>
    </div>

    <div class="panel">
      <button @click="$emit('setFps', fps + 1)" title="Speed up">
        <font-awesome-icon icon="plus" />
      </button>
      {{ fps }} fps
      <button @click="$emit('setFps', Math.max(1, fps - 1))" title="Slow down">
        <font-awesome-icon icon="minus" />
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'
import PatternLoader from './PatternLoader.vue'

@Component({
  components: {
    PatternLoader
  }
})
export default class ControlBar extends Vue {
  @Prop({ required: true }) running!: boolean
  @Prop({ required: true }) size!: number
  @Prop({ required: true }) fps!: number
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
.control-bar {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 16px;
  flex-wrap: wrap;
}

.panel {
  margin: 0 10px 15px 10px;
}

button {
  background-color: transparent;
  border: 0;
  outline: none;
  cursor: pointer;
  color: black;
  text-shadow: 0 0 5px 2px white;
  transition: all 0.2s ease;
  font-size: 16px;
}

button:hover {
  transform: scale(1.2);
}

button:active {
  transform: scale(0.8);
}
</style>
