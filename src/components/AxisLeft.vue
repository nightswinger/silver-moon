<script setup>
const { yScale } = defineProps({
  yScale: Object,
  width: Number
})

const textPadding = -20

let offset = typeof window !== "undefined" && window.devicePixelRatio > 1 ? 0 : 0.5
let k = -1
let tickSizeOuter = 6
let tickSizeInner = 6
let tickPadding = 3

let spacing = Math.max(tickSizeInner, 0) + tickPadding
let range = yScale.range()
let range0 = +range[0] + offset
let range1 = +range[range.length - 1] + offset
let pathD = "M" + k * tickSizeOuter + "," + range0 + "H" + offset + "V" + range1 + "H" + k * tickSizeOuter
</script>

<template>
  <g
    fill="none"
    font-size="10"
    font-family="sans-serif"
    text-anchor="end"
  >
    <path class="domain" stroke="currentColor" :d="pathD" />
    <g
      v-for="(d,i) in yScale.ticks(5)" :key="i"
      class="tick"
      opacity="1"
      :transform="`translate(0, ${yScale(d) + offset})`"
    >
      <line
        stroke="currentColor"
        :x2="k*tickSizeInner"
      ></line>
      <text
        fill="currentColor"
        dy=".32em"
        :x="k*spacing"
      >{{ d }}</text>
    </g>
  </g>
</template>