<template>
  <div id="app">
    <scale-screen>
      <HelloWorld msg="Welcome to Your Vue.js App"/>
      <div class="chart" ref="chart"></div>
    </scale-screen>
  </div>
</template>

<script>
  import ScaleScreen from '@/components/ScaleScreen/ScaleScreen'
import HelloWorld from './components/HelloWorld.vue'
import echarts from 'echarts'
export default {
  name: 'app',
  components: {
    ScaleScreen,
    HelloWorld
  },
  mounted () {
    let myChart = echarts.init(this.$refs['chart']);

    // 指定图表的配置项和数据
    let option = {
      title: {
        text: 'ECharts 入门示例'
      },
      tooltip: {},
      legend: {
        data:['销量']
      },
      xAxis: {
        data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
      },
      yAxis: {},
      series: [{
        name: '销量',
        type: 'bar',
        data: [5, 20, 36, 10, 10, 20]
      }]
    };

    // 使用刚指定的配置项和数据显示图表。
    myChart.setOption(option);
  }
}
</script>

<style>
body {
  margin: 0;
  text-align: center;
  background: black;
}
  .chart {
    width: 50%;
    height: 200px;
  }
</style>
