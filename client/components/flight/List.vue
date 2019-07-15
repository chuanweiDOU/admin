<template>
  <div>
    <h3>
      Flight <span>({{ list.length }} レグ搭乗中)</span>
    </h3>
    <!--
    <chart :chart-data="getChartDataset(list)" />
    -->
    <div class="flight">
      <div
        v-for="item in list"
        :key="item.id"
      >
        <div class="airline-tag">
          {{ timeFormat(item.data.time) }} {{ item.data.registration }} ({{ boardingType(item.data.boardingType) }})
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { getAirportName, getAirlineName, getBoardingTypeName, getTimeFormat } from '~/utils'
const Chart = () => import('./Chart.vue')

const YEARS: number[] = [
  2015,
  2016,
  2017,
  2018,
  2019
];

const LABEL_TEXT: string = 'Flights';

const COLOR_TEXT: string = '#42b883';

export default Vue.extend({
  props: {
    list: {
      type: Array
    },
    number: {
      type: Number
    }
  },
  components: {
    Chart
  },
  methods: {
    timeFormat(t) {
      return getTimeFormat(t)
    },
    airline(id) {
      return getAirlineName(id)
    },
    departure(id) {
      return getAirportName(id)
    },
    arrival(id) {
      return getAirportName(id)
    },
    boardingType(id) {
      return getBoardingTypeName(id)
    },
    getChartDataset(items) {
      let dataset: number[] = []
      for (let yearIndex = 0; yearIndex < YEARS.length; yearIndex++) {
        const size = items.filter(item => {
          return item.data.time.includes(YEARS[yearIndex]) === true
        }) || 0

        // console.log(YEARS[yearIndex] + ' : ' + size.length)
        dataset.push(size.length)
      }

      return {
        labels: YEARS,
        datasets: [
          {
            label: LABEL_TEXT,
            backgroundColor: COLOR_TEXT,
            data: dataset
          }
        ]
      }
    }
  }
})
</script>

<style scoped>
.flight {
  min-width: 400px;
  text-align: center;
}

.airline-tag {
  width: 100%;
  margin: 10px 12px;
}
</style>
