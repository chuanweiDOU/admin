<template>
    <div>
        <a href="#" class="click-button" @click="$emit('handleClick');">
            {{ text }}
        </a>
    </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
    props: {
        text: {
            type: String
        }
    }
})
</script>

<style lang="sass" scoped>
@import '../../assets/main.scss'
.click-button
    display: inline-block
    border: solid 1px $border-color
    background-color: #fff
    color: $normal-color
    font-size: 1.2em
    margin: 0 0 20px
    padding: 10px
    outline: none
    appearance: none
    -webkit-border-radius: 3px
    -moz-border-radius: 3px
    border-radius: 3px
.click-button::before,
.click-button::after
    position: absolute
    z-index: -1
    display: block
    content: ''
    -webkit-box-sizing: border-box
    -moz-box-sizing: border-box
    box-sizing: border-box
    -webkit-transition: all .3s
    transition: all .3s
</style>
