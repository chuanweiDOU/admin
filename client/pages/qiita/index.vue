<template>
  <main-template
    v-if="$store.state.qiita.qiitas"
    :user-status="$store.state.product.userStatus"
  >
    <main-template :is-form="isForm">
      <story-input
        v-model="search"
        placeholder="タイトル"
      />
    </main-template>
    <qiita-list
      :list="$store.state.qiita.qiitas"
      :search="search"
      :tag="tag"
    />
    <pagination
      :page="page"
      :max="Math.ceil(qiitas.length / 20)"
      @form-data="applyPage"
    />
  </main-template>
</template>

<script lang="ts">
import Vue from 'vue'
import { mapState } from 'vuex'
import { CATEGORIES } from '../../utils'
const MainTemplate = () => import('../../components/layout/MainTemplate.vue')
const QiitaList = () => import('../../components/qiita/List.vue')
const Pagination = () => import('../../components/layout/Pagination.vue')
const StoryInput = () => import('../../components/atoms/Input.vue')
const StorySelect = () => import('../../components/atoms/Select.vue')

export default Vue.extend({
    middleware: 'auth',
    components: {
        MainTemplate,
        QiitaList,
        Pagination,
        StoryInput,
        StorySelect
    },
    data () {
        return {
            tag: 1,
            search: '',
            page: 1,
            isForm: true
        }
    },
    computed: {
        ...mapState('product', [
            'userStatus'
        ]),
        ...mapState('qiita', [
            'qiitas'
        ]),
        categoryOptions () {
            let array: string[] = []
            CATEGORIES.forEach(category => {
                array.push(category.text)
            })
            return array
        }
    },
    async mounted() {
        await this.$store.dispatch('qiita/fetchQiitas', {
            'tag': 1,
            'search': '',
            'page': 1
        })
    },
    methods: {
        async getQiitaByTag () {
            await (this as any).$store.dispatch('qiita/fetchQiitas', {
                'tag': this.tag,
                'search': this.search,
                'page': this.page
            })
        },
        async applyPage(value) {
            this.page = value
            await this.getQiitaByTag()
        }
    }
})
</script>

<style scoped>

</style>
