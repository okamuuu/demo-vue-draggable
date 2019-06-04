<template>
  <div class="section">
    <div class="container">
      <div class="columns">
        <div class="column">
          <h1 class="title">Vue.Draggable <em>Swap</em> Demo</h1>
          <table class="table is-bordered" style="font-size:1.5em;">
            <thead>
              <tr>
                <th>id</th><th>name</th><td>age</td>
              </tr>
            </thead>
            <draggable v-model="items" tag="tbody" :move="handleMove" @end="handleDragEnd" :options="{animation:500}">
              <tr v-for="item in items" :key="item.id" :data-item-id="item.id">
                <td>{{ item.id }}</td><td>{{ item.name }}</td><td>{{ item.age }}</td>
              </tr>
            </draggable>
          </table>
        </div>
        <div class="column">
          <h2 class="title">this.items</h2>
          <p>{{ items }}</p>
          <br />
          <h2 class="title">this.items.map(x => x.id)</h2>
          <p style="font-size: 4em;"><em>{{ orders }}</em></p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
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
    },
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
      return false
    }
  }
}
</script>

<style scoped>
em {
  font-style: normal;
  background: linear-gradient(transparent 75%, #89BDDE 0%);
}

.ghost,
.sortable-chosen {
  color: #fff;
  background-color: #3273dc;
}
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
