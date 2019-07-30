<template>
    <div>
        <select
            :multiple="multiple"
            class="option-select"
            @input="$emit('handleSelect')"
        >
            <option
                v-for="(value, key) in options"
                :key="key"
                :value="key"
            >
                {{ value }}
            </option>
        </select>
    </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
    props: {
        options: {
            type: Array
        },
        multiple: {
            type: Boolean,
            default: false
        }
    }
})
</script>

<style lang="sass" scoped>
@import '../../assets/main.scss'
.option-select
    outline: none
    text-indent: 0.01px
    text-overflow: ''
    background: none transparent
    font-size: 1.2em
    margin: 0 0 20px
    padding: 10px
    width: 300px
    vertical-align: middle
    color: inherit
    -webkit-appearance: button
    -moz-appearance: button
    appearance: auto
.option-select::-ms-expand
    display: none
.option-select:-moz-focusring
    color: transparent
    text-shadow: 0 0 0 $border-color
</style>
