<template>
  <main-template
    v-if="tips && events && hosts"
    :user-status="userStatus"
  >
    <new-tip />
    <tip-list
      :list="tips.item"
      :number="page"
      :search="inputSearch"
    />
    <pagination
      :page="page"
      :max="Math.ceil(tips.item.length / 20)"
      @form-data="applyPage"
    />
    <!--
    <new-event />
    <host-list
      :list="hosts.item"
    />
    <new-host />
    -->
    <new-photo />
  </main-template>
</template>

<script lang="ts">
import Vue from 'vue'
import { mapState } from 'vuex'
const MainTemplate = () => import('../../components/layout/MainTemplate.vue')
const TipList = () => import('../../components/tip/List.vue')
const NewTip = () => import('../../components/tip/New.vue')
const NewEvent = () => import('../../components/event/New.vue')
const HostList = () => import('../../components/host/List.vue')
const NewHost = () => import('../../components/host/New.vue')
const NewPhoto = () => import('../../components/photo/New.vue')
const Pagination = () => import('../../components/layout/Pagination.vue')
const StoryInput = () => import('../../components/atoms/Input.vue')
const StorySelect = () => import('../../components/atoms/Select.vue')

export default Vue.extend({
    middleware: 'auth',
    components: {
        MainTemplate,
        TipList,
        NewTip,
        NewEvent,
        HostList,
        NewHost,
        NewPhoto,
        Pagination,
        StoryInput,
        StorySelect
    },
    async fetch({ store }) {
        await store.dispatch('product/fetchTips', null)
        await store.dispatch('product/fetchEvents')
        await store.dispatch('product/fetchHosts')
        await store.dispatch('product/fetchPhotos')
    },
    data () {
        return {
            page: 1,
            inputSearch: '',
            selectedEvent: 0,
            isForm: true
        }
    },
    computed: {
        ...mapState(mapState('product', [
            'userStatus',
            'tips',
            'hosts',
            'events'
        ])),
        eventOptions () {
            let array: string[] = [];
            this.$store.state.product.events.item.forEach((item) => {
                array.push(item.data.name)
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
