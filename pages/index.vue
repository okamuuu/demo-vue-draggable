<template>
  <div class="section">
    <div class="container">
      <div class="columns">
        <div class="column">
          <h1 class="title">Vue.Draggable Demo</h1>
          <table class="table is-bordered">
            <thead>
              <tr>
                <th>id</th><th>name</th><td>age</td>
              </tr>
            </thead>
            <draggable v-model="items" tag="tbody" @end="handleDragEnd" :options="{animation:500}">
              <tr class="movable" v-for="item in items" :key="item.id" :data-item-id="item.id">
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
          <p>{{ orders }}</p>
          <br />
          <h2 class="title">From/To</h2>
          <p>
            <b>From:</b> {{ from }}<br />
            <b>To:</b> {{ to }}
          </p>
        </div>
      </div>
      <br />

      <h2 class="title">Script</h2>
      <pre v-highlightjs><code class="javascript">
import draggable from "vuedraggable";

export default {
  components: {
    draggable,
  },
  data() {
    return {
      items: [
        { id: 1, name: "Bianka Effertz", age: 37 },
        { id: 2, name: "Mckayla Bogan", age: 20 },
        { id: 3, name: "Estevan Mann", age: 17 },
        { id: 4, name: "Cloyd Ziemann", age: 55 }
      ],
    };
  },
  methods: {
    handleDragEnd(e) {
      const { from , to } = e
      this.$toast.show('dragEnd')
      console.log("dragEnd")
      // console.log(e)
    },
  }
}
      </code></pre>
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
    return {
      items,
      from: null,
      to: null,
    };
  },
  computed: {
    orders() {
      return this.items.map(x => x.id)
    },
  },

  methods: {
    handleDragEnd(e) {
      const { newIndex, oldIndex } = e
      this.$toast.show('dragEnd')
      this.from = this.items[oldIndex]
      this.to = this.items[newIndex]
    },
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
