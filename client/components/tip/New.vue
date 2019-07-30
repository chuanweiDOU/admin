<template>
  <div v-if="events">
    <main-template :is-form="isForm">
      <story-input
        v-model="title"
        placeholder="タイトル"
      />
    </main-template>
    <main-template :is-form="isForm">
      <story-input
        v-model="url"
        placeholder="URL"
      />
    </main-template>
    <main-template :is-form="isForm">
      <story-input
        v-model="description"
        placeholder="詳細"
      />
    </main-template>
    <main-template :is-form="isForm">
      <story-select
        :options="categoryOptions"
        v-model="tags"
        name="タグ"
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
      <story-button
        text="Tipを追加"
        @handleClick="postTip"
      />
    </main-template>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { mapState } from 'vuex'
import dayjs from 'dayjs'
import { CATEGORIES } from '~/utils'
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
            title: '',
            url: '',
            description: '',
            tags: 0,
            event: 0,
            isForm: true
        }
    },
    computed: {
        ...mapState(mapState('product', [
            'events'
        ])),
        categoryOptions () {
            let array: string[] = []
            CATEGORIES.forEach((item) => {
                array.push(item.text)
            })
            return array
        },
        eventOptions () {
            let array: string[] = [];
            this.$store.state.product.events.item.forEach((item) => {
                array.push(item.data.name)
            })
            return array
        }
    },
    async created () {
        await this.$store.dispatch('product/fetchEvents')
    },
    methods: {
        applyTags (value) {
            this.tags = value
        },
        reset () {
            this.title = ''
            this.url = ''
            this.description = ''
            this.tags = 0
            this.event = 0
        },
        async postTip () {
            await (this as any).$store.dispatch('product/addTip', {
                title: this.title,
                url: this.url,
                description: this.description,
                tags: [this.tags],
                event: this.event,
                time: dayjs().format('')
            })
            this.reset()
        }
    }
})
</script>

<style scoped>

</style>
