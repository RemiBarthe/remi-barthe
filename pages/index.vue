<template>
  <div class="page-container">
    <div class="page-header">
      <h1 class="name-title">Rémi Barthe</h1>

      <div class="links">
        <StickyButton>
          <img alt="logo github" src="../assets/images/github.svg" />
        </StickyButton>

        <StickyButton>
          <img alt="logo at mail" src="../assets/images/at.svg" />
        </StickyButton>

        <StickyButton>
          <img alt="logo linkedin" src="../assets/images/linkedin.svg" />
        </StickyButton>
      </div>
    </div>

    <div class="presentation">
      <div class="title">
        <div class="title-decoration"></div>
        <h2>
          web_ <br />
          developer
        </h2>
      </div>
      <h3 class="subtitle">Lorem ipsum sit amet dolor loprem alork</h3>
    </div>

    <!-- <div class="pointers">
      <div
        v-for="pointer in pointers"
        v-show="showPointer"
        class="pointer"
        :style="[pointerPosition, pointerCss(pointer)]"
      ></div>

      <BackgroundForm />
    </div>

    <svg>
      <defs>
        <filter id="filter">
          <feGaussianBlur in="SourceGraphic" stdDeviation="8" result="blur" />
          <feColorMatrix
            in="blur"
            mode="matrix"
            values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 28 -10"
            result="filter"
          />
          <feComposite in="SourceGraphic" in2="filter" operator="atop" />
        </filter>
      </defs>
    </svg> -->
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { default as POINTERS, Pointer } from '@/plugins/pointers';
import '@/assets/style/global.scss';

export default defineComponent({
  name: 'HomePage',
  data: () => ({
    mousePointer: {
      x: 0,
      y: 0
    },
    showPointer: false,
    pointers: POINTERS
  }),
  computed: {
    pointerPosition(): string {
      return `transform: translateX(${this.mousePointer.x}px) translateY(${this.mousePointer.y}px);`;
    }
  },
  mounted() {
    document.addEventListener('mousemove', this.onMouseMove);
    document.addEventListener('mouseleave', () => this.hidePointer());
  },
  unmounted() {
    document.removeEventListener('mousemove', this.onMouseMove);
    document.removeEventListener('mouseleave', this.hidePointer());
  },
  methods: {
    onMouseMove(event: MouseEvent) {
      this.showPointer = true;
      this.mousePointer.x = event.pageX - 11;
      this.mousePointer.y = event.pageY - 11;
    },
    pointerCss(pointer: Pointer): string {
      return `
      width: ${pointer.size}px;
      height: ${pointer.size}px;
      transition-duration: ${pointer.transitionDuration * 2}s;
      margin-top: ${pointer.margin}px;
      margin-left: ${pointer.margin}px;
      `;
    },
    hidePointer() {
      setTimeout(() => {
        this.showPointer = false;
      }, 250);
    }
  }
});
</script>

<style lang="scss" scoped>
.page-container {
  padding: 20px 80px;
  height: calc(100vh - 40px);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  .page-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    .name-title {
      font-size: 1.5rem;
      font-family: 'ZenKakuBlack';
    }
    .links {
      display: flex;
      transform: rotate(5.45deg);
      cursor: pointer;
    }
  }
  .presentation {
    display: flex;
    flex-flow: column wrap;
    align-content: center;
    align-items: flex-end;
    .title {
      font-size: 6rem;
      font-family: 'LeagueSpartan';
      display: flex;

      h2 {
        margin: 0;
      }
    }
    .title-decoration {
      width: 30px;
      height: 140px;
      background-color: #4062bb;
      margin-right: 40px;
    }
    .subtitle {
      font-size: 1.5rem;
      font-family: 'ZenKakuBold';
      text-align: right;
    }
  }
  .pointers {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    filter: url('#filter');
    .pointer {
      position: absolute;
      top: 0;
      left: 0;
      pointer-events: none;
      will-change: transform;
      border-radius: 50px;
      backface-visibility: hidden;
      background-color: #4062bb;
      transition: transform cubic-bezier(0.175, 0.885, 0.32, 1.275);
    }
  }
}
</style>
