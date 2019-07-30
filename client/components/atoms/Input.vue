<template>
    <div>
        <input
            :type="inputType"
            :placeholder="placeholder"
            class="text-input"
            @input="updateInput"
        />
    </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
    props: {
        placeholder: {
            type: String
        },
        inputType: {
            type: String
        }
    },
    methods: {
        updateInput(event: any) {
            this.$emit('handleInput', event.target.value)
        }
    }
})
</script>

<style lang="sass" scoped>
@import '../../assets/main.scss'
.text-input
    border: solid 1px $border-color
    color: $normal-color
    font-size: 1.2em
    margin: 0 0 20px
    padding: 10px
    width: 300px
    -webkit-border-radius: 3px
    -moz-border-radius: 3px
    border-radius: 3px
.text-input:focus
    border: solid 1px $normal-color
</style>
