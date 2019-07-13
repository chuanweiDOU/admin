<template>
  <div>
    <main-template :is-form="isForm">
      <story-input
        v-model="form.name"
        placeholder="名前"
      />
    </main-template>
    <main-template :is-form="isForm">
      <story-input
        v-model="form.url"
        placeholder="URL"
      />
    </main-template>
    <main-template :is-form="isForm">
      <story-select
        :options="localeOptions"
        v-model="form.locale"
      />
    </main-template>
    <main-template :is-form="isForm">
      <story-button
        text="Eventを追加"
        @click="postEvent"
      />
    </main-template>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { mapState } from 'vuex'
import { LOCALES } from '~/utils'
const MainTemplate = () => import('~/components/layout/MainTemplate.vue')
const StoryInput = () => import('~/components/atoms/Input.vue')
const StorySelect = () => import('~/components/atoms/Select.vue')
const StoryButton = () => import('~/components/atoms/Button.vue')

export default Vue.extend({
    components: {
        MainTemplate,
        StoryInput,
        StorySelect,
        StoryButton
    },
    data () {
        return {
            form: {
                id: 0,
                name: '',
                url: '',
                locale: 0
            },
            isForm: true
        }
    },
    computed: {
        ...mapState(mapState('product', [
            'events'
        ])),
        localeOptions () {
            let array: string[] = []
            LOCALES.forEach(locale => {
                array.push(locale.text)
            })
            return array
        }
    },
    methods: {
        reset () {
            this.form.name = ''
            this.form.url = ''
            this.form.locale = 0
        },
        async postEvent () {
            await (this as any).$store.dispatch('product/addEvent', {
                name: this.form.name,
                url: this.form.url,
                locale: this.form.locale
            })
            this.reset()
        }
    }
})
</script>

<style scoped>

</style>
