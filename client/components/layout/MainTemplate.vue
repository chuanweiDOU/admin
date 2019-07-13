<template>
  <div>
    <LeftMenu
      v-if="userStatus"
    />
    <div
      v-if="userStatus"
      class="logout"
    >
      <story-button
        text="logout"
        @click="logout"
      />
    </div>
    <div :class="isForm ? `form` : `main`">
      <slot />
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
const LeftMenu = () => import('~/components/layout/LeftMenu.vue')
const StoryButton = () => import('~/components/atoms/Button.vue')

export default Vue.extend({
    props: {
        userStatus: {
            type: Boolean
        },
        isForm: {
            type: Boolean
        }
    },
    components: {
        LeftMenu,
        StoryButton
    },
    methods: {
        async logout() {
            await (this as any).$store.dispatch('product/signOut')
            if (!(this as any).$store.state.product.userStatus) {
                this.$router.push('/login')
            }
        }
    }
})
</script>

<style scoped>
.logout {
  text-align: right;
  margin-bottom: 15px;
}

.form {
  margin: 0 auto;
  padding-bottom: 10px;
}
</style>
