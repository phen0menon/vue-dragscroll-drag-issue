<template>
  <Draggable @setDraggable="setDraggable">
    <div
      class="flex"
      :class="{active: item.active}"
      v-for="item in items"
      :key="item.title"
      @mouseup="select(item.title)"
    >{{item.title}}</div>
  </Draggable>
</template>

<style>
.flex {
  height: 200px;
  width: 250px;
  background: #ccc;
  border-radius: 20px;
  border: 1px solid #FA4E05;
  margin: 0 10px;
}

.active {
  color: blue;
  background: red;
}
</style>


<script>
import Draggable from "~/components/Draggable.vue";

export default {
  components: {
    Draggable
  },
  data() {
    return {
      dragging: false,
      items: [
        { title: "a", active: false },
        { title: "b", active: false },
        { title: "c", active: false },
        { title: "d", active: false },
        { title: "f", active: false },
        { title: "g", active: false }
      ]
    };
  },
  methods: {
    select(title) {
      if (!this.dragging) {
        const item = this.items.find(i => i.title === title);
        item.active = !item.active;
      }
    },

    setDraggable(flag) {
      this.dragging = flag;
    }
  }
};
</script>
