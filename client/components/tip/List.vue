<template>
  <div>
    <h3>
      Tip <span>{{ list.length }} 件登録中</span>
    </h3>
    <div
      v-for="item in list"
      :key="item.id"
      class="tip"
    >
      <div
        v-if="item.page === number"
        class="tip-tag"
      >
        <h2>
          <a
            :href="item.data.url"
            target="_blank"
            rel="noopener"
          >
            {{ item.data.title }}
          </a>
          <span>
          {{ diffTime(item.data.time) }}
        </span>
        </h2>
        <!--
        <span
          v-for="(tag, index) in item.data.tags"
          :key="index"
        >
          <story-label :text="getText(tag)" />
        </span>
        <div
          v-if="item.data.description"
          class="description"
        >
          {{ item.data.description }}
        </div>
        -->
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { getDiffTime } from '~/utils'
const StoryLabel = () => import('~/components/atoms/Label.vue')

export default Vue.extend({
    props: {
        list: {
            type: Array
        },
        type: {
            type: Array
        },
        number: {
            type: Number
        },
        search: {
            type: String
        }
    },
    components: {
        StoryLabel
    },
    methods: {
        diffTime(t) {
            return getDiffTime(t)
        }
    }
})
</script>

<style scoped>
.tip {
  min-width: 400px;
  text-align: center;
}

.tip-tag {
  width: 100%;
  margin: 10px 12px;
}

h2 {
  font-size: 18px;
}

h2 a {
  color: #808080;
  text-decoration: none;
}

h2 span {
  float: right;
}

.description {
  margin-bottom: 20px;
  font-size: 12px;
  color: #00008b;
}
</style>
