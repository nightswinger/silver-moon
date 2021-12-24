<script setup>
import { scaleLinear } from 'd3-scale'
import { extent } from 'd3-array'
import { line } from 'd3-shape'
import XAxis from './XAxis.vue'
import AxisLeft from './AxisLeft.vue'
import { axisLeft } from 'd3-axis'

const { data } = defineProps({ data: Array })

const w = 400
const h = 400
const margin = {
  top: 40,
  bottom: 40,
  left: 40,
  right: 40
}

const width = w - margin.right - margin.left
const height = h - margin.top - margin.bottom

const xScale = scaleLinear()
  .domain(extent(data, d => d.x))
  .range([0, width])
const yScale = scaleLinear()
  .domain(extent(data, d => d.y))
  .range([height, 0])

const lineFunction = line()
  .x(d => xScale(d.x))
  .y(d => yScale(d.y))

</script>

<template>
  <div>
    <svg :width="w" :height="h">
      <g :transform="`translate(${margin.left},${margin.top})`">
        <AxisLeft :y-scale="yScale" :width="width" />
        <path :d="lineFunction(data)" stroke="black" fill="none"></path>
      </g>
    </svg>
  </div>
</template>