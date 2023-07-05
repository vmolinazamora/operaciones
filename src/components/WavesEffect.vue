<template>
  <div>
    <svg
      class="waves"
      xmlns="http://www.w3.org/2000/svg"
      xmlns:xlink="http://www.w3.org/1999/xlink"
      viewBox="0 24 150 28"
      preserveAspectRatio="none"
      shape-rendering="auto"
    >
      <defs>
        <path
          id="gentle-wave"
          d="M-160 44c30 0 58-18 88-18s 58 18 88 18 58-18 88-18 58 18 88 18 v44h-352z"
        />
      </defs>
      <g class="parallax">
        <use
          v-for="(wave, index) in waves.waves"
          :key="index"
          xlink:href="#gentle-wave"
          :x="wave.x"
          :y="wave.y"
          :fill="
            'rgba(' +
            waves.color.r +
            ',' +
            waves.color.g +
            ',' +
            waves.color.b +
            ',' +
            (1 / waves.waves.length) * (index + 1) +
            ')'
          "
          :style="{
            'animation-delay': wave.delay + 's',
            'animation-duration': wave.duration + 's',
          }"
        />
      </g>
    </svg>
  </div>
</template>

<style>
.waves {
  position: relative;
  width: 100%;
  height: 15vh;
  margin-bottom: -7px; /*Fix for safari gap*/
  min-height: 100px;
  max-height: 150px;
}

.parallax > use {
  animation: move-forever 25s cubic-bezier(0.55, 0.5, 0.45, 0.5) infinite;
}

@keyframes move-forever {
  0% {
    transform: translate3d(-90px, 0, 0);
  }
  100% {
    transform: translate3d(85px, 0, 0);
  }
}

@media (max-width: 768px) {
  .waves {
    height: 40px;
    min-height: 40px;
  }
}
</style>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "WavesEffect",
  props: { waves: { type: Object, defaul: {} } },
  setup(props) {
    //return {};
    //console.log(props.waves);
  },
});
</script>
