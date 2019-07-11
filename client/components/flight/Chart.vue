<script lang="ts">
import Vue from 'vue'
import ChartData from 'chart.js'
import { Bar } from 'vue-chartjs'

const OPTION: ChartData.ChartOptions = {
  responsive: true,
  maintainAspectRatio: false,
  scales: {
    yAxes: [
      {
        ticks: {
          beginAtZero: true,
          min: 0,
          max: 40
        }
      }
    ]
  }
};

export default Vue.extend({
  extends: Bar,
  props: {
    chartData: {
      type: Object
    }
  },
  methods: {
    mounted () {
      this.renderChart(this.chartData, OPTION)
    }
  }
})
</script>
