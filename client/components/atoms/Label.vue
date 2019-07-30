<template>
    <div
        :style="`background-color: ${backgroundColor}; color: ${color};`"
        class="text-label"
    >
        <label>{{ text }}</label>
        <slot />
    </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
    props: {
        text: {
            type: String
        },
        backgroundColor: {
            type: String,
            default: '#fff'
        },
        color: {
            type: String,
            default: '#000'
        }
    }
})
</script>

<style lang="sass" scoped>
@import '../../assets/main.scss'
.text-label
    border: solid 1px $border-color
    text-align: center
    font-size: 1.2em
    margin: 0 12px 8px
    padding: 8px
    width: 160px
    -webkit-border-radius: 3px
    -moz-border-radius: 3px
    border-radius: 3px
</style>
