<template>
  <div v-if="events">
    <main-template :is-form="isForm">
      <story-input
        v-model="name"
        placeholder="イベント名"
      />
    </main-template>
    <main-template :is-form="isForm">
      <story-select
        :options="eventOptions"
        v-model="event"
        name="イベント"
      />
    </main-template>
    <main-template :is-form="isForm">
      <story-input
        v-model="location"
        placeholder="場所"
      />
    </main-template>
    <main-template :is-form="isForm">
      <story-select
        :options="localeOptions"
        v-model="locale"
      />
    </main-template>
    <main-template :is-form="isForm">
      <story-input
        v-model="participants"
        placeholder="参加者数"
      />
    </main-template>
    <main-template :is-form="isForm">
      <story-input
        v-model="max_participants"
        placeholder="最大参加者数"
      />
    </main-template>
    <main-template :is-form="isForm">
      <story-input
        v-model="lt"
        placeholder="登壇・LT数"
      />
    </main-template>
    <main-template :is-form="isForm">
      <story-button
        text="Hostを追加"
        @handleClick="postHost"
      />
    </main-template>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { mapState } from 'vuex'
import { CATEGORIES, LOCALES } from '~/utils'
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
            name: '',
            event: 0,
            location: '',
            locale: 0,
            participants: '',
            max_participants: '',
            lt: '',
            isForm: true
        }
    },
    computed: {
        ...mapState(mapState('product', [
            'events'
        ])),
        categoryOptions () {
            let array: string[] = []
            CATEGORIES.forEach(category => {
                array.push(category.text)
            })
            return array
        },
        localeOptions () {
            let array: string[] = []
            LOCALES.forEach(locale => {
                array.push(locale.text)
            })
            return array
        },
        eventOptions () {
            let array: string[] = []
            this.$store.state.product.events.item.forEach((item) => {
                array.push(item.data.name)
            })
            return array
        }
    },
    async created () {
        await (this as any).$store.dispatch('product/fetchEvents')
    },
    methods: {
        reset () {
            this.name = ''
            this.event = 0
            this.location = ''
            this.locale = 0
            this.participants = ''
            this.max_participants = ''
            this.lt = ''
        },
        async postHost () {
            await (this as any).$store.dispatch('product/addHost', {
                name: this.name,
                event: this.event,
                location: this.location,
                locale: this.locale,
                participants: this.participants,
                max_participants: this.max_participants,
                lt: this.lt
            })
            this.reset()
        }
    }
})
</script>

<style scoped>

</style>
