<template>
  <div class="menu">
    <div
      v-for="value in menu"
      :key="value.title"
    >
      <nuxt-link
        :to="value.url"
      >
        <img
          :src="'/' + value.src"
          :alt="value.src"
          decoding="async"
        >
      </nuxt-link>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { MENU_LIST } from '~/utils'

export default Vue.extend({
    data () {
        return {
            menu: MENU_LIST
        }
    }
})
</script>

<style scoped>
.menu {
  top: 5%;
  left: 5%;
  display: flex;
}

img {
  width: 25px;
  height: 25px;
  margin: 15px;
}
</style>
