<template>
  <main-template
    :user-status="$store.state.product.userStatus"
    class="login"
  >
    <main-template :is-form="isForm">
      <story-input
        v-model="email"
        placeholder="Email"
      />
    </main-template>
    <main-template :is-form="isForm">
      <story-input
        v-model="password"
        input-type="password"
        placeholder="Password"
      />
    </main-template>
    <main-template :is-form="isForm">
      <story-button
        text="login"
        @handleClick="login"
      />
    </main-template>
  </main-template>
</template>

<script lang="ts">
import Vue from 'vue'
import { mapState } from 'vuex'
const MainTemplate = () => import('~/components/layout/MainTemplate.vue')
const StoryInput = () => import('~/components/atoms/Input.vue')
const StoryButton = () => import('~/components/atoms/Button.vue')

export default Vue.extend({
    components: {
        MainTemplate,
        StoryInput,
        StoryButton
    },
    data () {
        return {
            email: '',
            password: '',
            isForm: true
        }
    },
    computed: {
        ...mapState(mapState('product', [
            'userStatus'
        ]))
    },
    methods: {
        async login () {
            await this.$store.dispatch('product/signIn', {
                email: this.email,
                password: this.password
            })

            if (this.$store.state.product.userStatus) {
                await this.$router.push('/')
            }
        }
    }
})
</script>

<style scoped>
.login {
  display: flex;
  min-height: 100vh;
  justify-content: center;
  align-items: center;
  text-align: center;
}
</style>
