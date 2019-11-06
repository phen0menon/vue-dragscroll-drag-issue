<template>
  <vuescroll :ops="options" @handle-scroll="dragstart">
    <div class="child">
      <slot/>
    </div>
  </vuescroll>
</template>

<style scoped>
.child {
  display: flex;
  outline: none;
  -ms-overflow-style: none;
  scrollbar-width: none;
  overflow-x: auto;
}
.child::-webkit-scrollbar {
  display: none;
}
</style>

<script>
import vuescroll from "vuescroll";

export default {
  components: {
    vuescroll
  },
  props: {
    setDraggable: {
      type: Function,
      default: () => {},
      required: false
    }
  },
  data() {
    return {
      currPos: 0,
      options: {
        vuescroll: {
          mode: "slide",
          zooming: false,
          // NOTE
          // Comment property 'scroller' below to see the problem
          scroller: {
            bouncing: {
              left: 0,
              right: 0,
              top: 0,
              bottom: 0
            },
            speedMultiplier: 0.9
          }
        },
        scrollPanel: {
          scrollingY: false
        },
        bar: {
          disable: true
        }
      }
    };
  },
  methods: {
    dragstart(vert, horiz, nativeEvent) {
      if (this.currPos === horiz.process) {
        this.$emit("setDraggable", false);
      } else {
        this.currPos = horiz.process;
        this.$emit("setDraggable", true);
      }
    }
  }
};
</script>
