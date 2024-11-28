<script setup lang="ts">
import { BarChart, LineChart } from 'echarts/charts'
import { GridComponent, LegendComponent, TitleComponent, TooltipComponent } from 'echarts/components'
import { use } from 'echarts/core'
import { CanvasRenderer } from 'echarts/renderers'
import { provide, ref } from 'vue'
import VChart, { THEME_KEY } from 'vue-echarts'

defineOptions({
  name: 'IndexPage',
})
use([CanvasRenderer, LineChart, TitleComponent, TooltipComponent, LegendComponent, GridComponent, BarChart])
provide(THEME_KEY, 'light')
const sheetOption = ref({
  legend: {
    selectedMode: false,
  },
  xAxis: {
    type: 'category',
    data: ['11.02', '11.03', '11.04'],
  },
  tooltip: {
    trigger: 'axis',
  },
  yAxis: {
    type: 'value',
  },
  series: [{
    name: '高压',
    data: [100, 299, 399],
    type: 'line',
    areaStyle: {
      color: '#71bbff',
    },
    smooth: true,
  }, {
    name: '低压',
    data: [10, 29, 39],
    type: 'line',
    areaStyle: {
      color: '#fcff64',
    },
    smooth: true,
  }],
})

function changeTo() {
  sheetOption.value.series.length = 0

  sheetOption.value.series = [{
    name: '心率',
    data: [69, 2, 5],
    type: 'line',
    areaStyle: {
      color: '#fcff64',
    },
    smooth: true,
  }]
}
</script>

<template>
  <button @click="changeTo" />
  <div class="h50vh flex justify-center">
    <VChart class="h50vh" :option="sheetOption" />
  </div>
  <button @click="changeTo">
    点我改变
  </button>
</template>

<route lang="yaml">
meta:
  layout: home
</route>
