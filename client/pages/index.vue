<template>
  <main-template
    v-if="contacts"
    :user-status="userStatus"
  >
    <contact-list
      :list="contacts.item"
      :number="contact"
    />
    <pagination
      :page="contact"
      :max="Math.ceil(contacts.item.length / 20)"
      @form-data="applyPageInContact"
    />
  </main-template>
</template>

<script lang="ts">
import Vue from 'vue'
import { mapState } from 'vuex'
import { CONTACT_CATEGORIES } from '../utils'
const MainTemplate = () => import('../components/layout/MainTemplate.vue')
const ContactList = () => import('../components/contact/List.vue')
const Pagination = () => import('../components/layout/Pagination.vue')
const StorySelect = () => import('../components/atoms/Select.vue')

export default Vue.extend({
    middleware: 'auth',
    components: {
        MainTemplate,
        ContactList,
        Pagination,
        StorySelect
    },
    async asyncData({ store }) {
        await store.dispatch('product/fetchContacts')
    },
    computed: {
        ...mapState('product', [
            'userStatus',
            'contacts'
        ]),
        contactCategoryOptions () {
            let array: string[] = []
            CONTACT_CATEGORIES.forEach(category => {
                array.push(category.text)
            })
            return array
        }
    },
    data () {
        return {
            event: 0,
            contact: 1,
            contactCategory: 0,
            isForm: true
        }
    },
    methods: {
        applyPageInContact(value) {
            this.contact = value
        }
    }
})
</script>

<style scoped>

</style>
