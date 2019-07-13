<template>
  <main-template
    v-if="flights"
    :user-status="userStatus"
  >
    <new-flight />
    <flight-list
      :list="flights.item"
      :number="page"
    />
    <pagination
      :page="page"
      :max="Math.ceil(flights.item.length / 20)"
      @form-data="applyPage"
    />
  </main-template>
</template>

<script lang="ts">
import Vue from 'vue'
import { mapState } from 'vuex'
import { BOARDING_TYPE_LIST } from '../../utils'
const MainTemplate = () => import('../../components/layout/MainTemplate.vue')
const FlightList = () => import('../../components/flight/List.vue')
const NewFlight = () => import('../../components/flight/New.vue')
const Pagination = () => import('../../components/layout/Pagination.vue')
const StorySelect = () => import('../../components/atoms/Select.vue')

export default Vue.extend({
    middleware: 'auth',
    components: {
        MainTemplate,
        Pagination,
        FlightList,
        NewFlight,
        StorySelect
    },
    async fetch({ store }) {
        await store.dispatch('product/fetchFlights', {
            boardingType: 0,
            year: 0
        })
    },
    data () {
        return {
            page: 1,
            selectedYaer: 2019,
            selectedBoardingType: 0,
            isForm: true
        }
    },
    computed: {
        ...mapState(mapState('product', [
            'userStatus',
            'flights'
        ])),
        boardingTypeOptions () {
            let array: string[] = []
            BOARDING_TYPE_LIST.forEach(category => {
                array.push(category.text)
            })
            return array
        }
    },
    methods: {
        applyPage(value) {
            this.page = value
        }
    }
})
</script>

<style scoped>

</style>
