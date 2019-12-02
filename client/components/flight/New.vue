<template>
    <div style="width: 100%;">
        <j-input
            placeholder="搭乗時間"
            input-type="text"
            style="text-align: left; margin: 12px;"
            @handleInput="applyTime"
        ></j-input>
        <div style="display: flex; justify-content: flex-start; margin: 12px;">
            <j-select
                    :options="airportOptions"
                    :multiple="Boolean(false)"
                    :selected-values="form.departure"
                    @handleSelect="applyDeparture"
            ></j-select>
            <j-select
                    :options="airportOptions"
                    :multiple="Boolean(false)"
                    :selected-values="form.arrival"
                    @handleSelect="applyArrival"
            ></j-select>
            <j-select
                    :options="airlineOptions"
                    :multiple="Boolean(false)"
                    :selected-values="form.airline"
                    @handleSelect="applyAirline"
            ></j-select>
            <j-select
                    :options="boardingTypeOptions"
                    :multiple="Boolean(false)"
                    :selected-values="form.boardingType"
                    @handleSelect="applyBoardingType"
            ></j-select>
        </div>
        <j-input
            placeholder="レジ"
            input-type="text"
            style="text-align: left; margin: 12px;"
            @handleInput="applyRegistration"
        ></j-input>
        <div style="text-align: right;">
            <j-button
                    text="Flightを追加"
                    variant-style="text"
                    style="margin: 12px;"
                    @handleClick="postFlight"
            ></j-button>
        </div>
    </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { addFlight } from '~/services/flightService'
import { AIRPORT_LIST, AIRLINE_LIST, BOARDING_TYPE_LIST } from '~/utils/flight'

export default Vue.extend({
    data() {
        return {
            form: {
                time: '' as string,
                departure: 0 as number,
                arrival: 0 as number,
                airline: 0 as number,
                boardingType: 0 as number,
                registration: '' as string
            },
            isForm: true as boolean
        }
    },
    computed: {
        airportOptions() {
            return AIRPORT_LIST
        },
        airlineOptions() {
            return AIRLINE_LIST
        },
        boardingTypeOptions() {
            return BOARDING_TYPE_LIST
        },
    },
    methods: {
        applyTime(value) {
            this.form.time = value
        },
        applyDeparture(value) {
            this.form.departure = value
        },
        applyArrival(value) {
            this.form.arrival = value
        },
        applyAirline(value) {
            this.form.airline = value
        },
        applyBoardingType(value) {
            this.form.boardingType = value
        },
        applyRegistration(value) {
            this.form.registration = value
        },
        reset () {
            this.form.time =''
            this.form.departure = 0
            this.form.arrival = 0
            this.form.airline = 0
            this.form.boardingType = 0
            this.form.registration = ''
        },
        async postFlight () {
            await addFlight(this.form)
            this.reset()
        }
    }
})
</script>
