<template>
  <div id="read" class="post">
    <img :src="post.imageUrl" class="post-img">
    <b-loading v-model="loading" />

    <transition name="animate_bounce">
      lol
    </transition>

    <div
      :class="[
        'card', 'post-content', 'animate__animated animate__bounceIn',
        post.imageUrl ? 'post-negmt' : ''
      ]"
    >
      <div v-show="!loading" class="card-content">
        <div class="title oswald">
          {{ post.title }}

          <b-dropdown v-if="$auth.loggedIn" aria-role="list" style="float: right">
            <b-button slot="trigger" slot-scope="{ active }" class="is-primary">
              <b-icon :icon="active ? 'chevron-up' : 'chevron-down'" />
            </b-button>

            <b-dropdown-item aria-role="listitem">
              Edit
            </b-dropdown-item>

            <b-dropdown-item
              aria-role="listitem"
              @click="deletePost"
            >
              Delete
            </b-dropdown-item>
          </b-dropdown>
        </div>

        <div class="subtitle">
          {{ post.author.fullName }} &middot; {{ prettyDate(post.createdAt) }}
        </div>

        <div>
          <markdown-it-vue :content="content" class="md-body" />
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, ref, useContext } from '@nuxtjs/composition-api'
import moment from 'moment'

export default defineComponent({
  name: 'read',

  setup (_, { root }) {
    const route = root.$route
    const { $axios } = useContext()
    const loading = ref(true)

    const post = ref({
      id: Number,
      author: Object,
      title: String,
      content: String,
      createdAt: String,
      updatedAt: String
    })

    const content = ref('')

    onMounted(async () => {
      const resp = await $axios.$get(`https://zeth-juno.herokuapp.com/post/${route.params.id}`)
      post.value = resp.post
      content.value = resp.post.content

      setTimeout(() => {
        loading.value = false
      }, 250)
    })

    function deletePost () {
      $axios.$delete(`https://zeth-juno.herokuapp.com/post/${route.params.id}`)
      root.$router.replace({ name: 'index' })
    }

    function prettyDate (date: string) {
      return moment.utc(date).format('MMM do, YYYY')
    }

    return {
      post,
      content,
      prettyDate,
      deletePost,
      loading
    }
  }
})
</script>

<style lang="scss" scoped>
#read {
  .post {
    &-img {
      -webkit-clip-path: polygon(0 0, 100% 0, 100% 92%, 0 100%);
      clip-path: polygon(0 0, 100% 0, 100% 92%, 0 100%);
      height: 70vh;
      width: 100%;
      object-fit: cover;
    }

    &-content {
      border-radius: 1em;
      max-width: 75em;
      width: 95%;
      min-height: 12em;
      margin: 0 auto;

      padding-left: 2em;
      padding-right: 2em;
      padding-top: 2em;
      padding-bottom: 1em;
    }

    &-negmt {
      margin-top: -20em;
    }
  }
}
</style>
