<template>
  <div class="section">
    <div class="container">
      <h2 class="title">template</h2>
      <pre v-highlightjs><code class="html">{{ template }}</code></pre>
      <br />
      <h2 class="title">script</h2>
      <pre v-highlightjs><code class="javascript">
import draggable from "vuedraggable";

export default {
  components: {
    draggable,
  },
  data() {
    const items = [
      { id: 1, name: "Bianka Effertz", age: 37 },
      { id: 2, name: "Mckayla Bogan", age: 20 },
      { id: 3, name: "Estevan Mann", age: 17 },
      { id: 4, name: "Cloyd Ziemann", age: 55 }
    ]
    return { items }
  },
  computed: {
    orders() {
      return this.items.map(x => x.id)
    }
  },

  methods: {
    handleDragEnd() {
      this.$toast.show('dragEnd')

      this.futureItem = this.items[this.futureIndex]
      this.movingItem = this.items[this.movingIndex]
      const _items = Object.assign([], this.items)
      _items[this.futureIndex] = this.movingItem
      _items[this.movingIndex] = this.futureItem

      this.items = _items
    },
    handleMove(e) {
      const { index, futureIndex } = e.draggedContext
      this.movingIndex = index
      this.futureIndex = futureIndex
      return false // disable sort
    }
}
      </code></pre>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    const template = `
<template>
  <table>
    <draggable v-model="items" tag="tbody" :move="handleMove" @end="handleDragEnd" :options="{animation:500}">
      <tr v-for="item in items" :key="item.id">
        <td>{{ item.id }}</td><td>{{ item.name }}</td><td>{{ item.age }}</td>
      </tr>
    </draggable>
  </table>
</template>
`;
    return { template }
  }
}
</script>

<style scoped>
.movable {
  cursor: move;
}
p {
   transition: width 2s;
}
p, pre {
  font-size: 1.5em;
}
</style>
