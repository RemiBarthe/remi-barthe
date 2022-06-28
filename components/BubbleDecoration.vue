<template>
  <div
    class="bubbles"
    ref="bubbleContainer"
    @mousemove="decorationMouve"
    @mouseleave="decorationHover = false"
    :style="decorationPosition"
  >
    <div v-for="i in 105"></div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'BubbleDecoration',
  data: () => ({
    decorationX: 0,
    decorationY: 0,
    decorationHover: false
  }),
  computed: {
    decorationPosition(): string {
      if (this.decorationHover)
        return `transform: translateX(${this.decorationX}px) translateY(${this.decorationY}px);`;

      return '';
    }
  },
  methods: {
    decorationMouve(event: MouseEvent) {
      const decorationPosition = {
        width: this.$refs.bubbleContainer.clientWidth,
        height: this.$refs.bubbleContainer.clientHeight,
        left: this.$refs.bubbleContainer.getBoundingClientRect().left,
        top: this.$refs.bubbleContainer.getBoundingClientRect().top
      };

      this.decorationHover = true;
      this.decorationX =
        (event.x - decorationPosition.left - decorationPosition.width / 2) / 7;
      this.decorationY =
        (event.y - decorationPosition.top - decorationPosition.height / 2) / 7;
    }
  }
});
</script>

<style lang="scss" scoped>
.bubbles {
  display: flex;
  gap: 40px;
  flex-flow: row wrap;
  max-width: 1000px;
  padding: 60px 40px;
  will-change: transform;
  transition: cubic-bezier(0.175, 0.885, 0.32, 1.275) 0.3s;
  border-radius: 50px;

  div {
    height: 8px;
    width: 8px;
    background-color: #59c3c3;
    border-radius: 50%;
  }
}
</style>
