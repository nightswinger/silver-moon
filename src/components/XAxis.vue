<script setup>
defineProps({
  xScale: Object,
  height: Number
})

const textPadding = 10
</script>

<template>
  <g fill="none">
    <g v-for="(d,i) in xScale.ticks(5)" :key="i">
      <line
        :y1="0"
        :y2="height"
        :x1="xScale(d)"
        :x2="xScale(d)"
        :style='{ stroke: "#e4e5eb" }'
      />
      <text
        dy=".71em"
        :x="xScale(d)"
        :y="height + textPadding"
        :style='{ textAnchor: "middle", fontSize: 12 }'
      >{{ d }}</text>
    </g>
  </g>
</template>