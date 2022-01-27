<template>
  <div class="pattern-loader">
    <form @submit="loadPattern">
      <select v-model="selectedPattern" required>
        <option v-for="p in patterns" :key="p" :value="p">{{ p }}</option>)
      </select>
      <button type="submit" title="Load pattern">
        <font-awesome-icon icon="upload" />
      </button>
    </form>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'

@Component({})
export default class PatternLoader extends Vue {
  @Prop({ required: false }) rows!: boolean[][]
  selectedPattern = ''
  patterns = [
    'period48glidergun',
    'smallspaceship',
    'spider'
  ]

  loadPattern (e: Event): void {
    e.preventDefault()
    if (!this.selectedPattern) return
    this.$emit('loadPattern', this.selectedPattern)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
select {
  height: 26px;
  padding: 2px;
  font-size: 14px;
  margin-bottom: 4px;
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
