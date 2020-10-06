<template>
  <div id="index">
    <section class="hero">
      <div v-if="posts.length > 0" class="hero-body">
        <div class="container">
          <div class="subtitle oswald header">
            Latest Posts

            <a class="header-right">
              View All
              <b-icon icon="view-list" />
            </a>
          </div>
          <hr>

          <div class="columns">
            <div
              v-for="post in posts.slice(0, 3)"
              :key="post.id"

              class="column"
            >
              <Post
                :id="post.id"
                :title="post.title"
                :image="post.imageUrl"
                :date="post.createdAt"
                :name="user.fullName"
              />
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, ref, useContext } from '@nuxtjs/composition-api'

import Post from '~/components/Index/Post.vue'

export default defineComponent({
  name: 'index',
  components: {
    Post
  },

  setup () {
    const { $axios } = useContext()

    const user = ref({
      bio: String,
      email: String,
      fullName: String,
      joinedAt: String,
      posts: []
    })

    const posts = ref([])

    onMounted(async () => {
      const resp = await $axios.$get('https://zeth-juno.herokuapp.com/user/zeth.leonardo@protonmail.com?includePosts=true')
      user.value = resp.user
      posts.value = resp.user.posts.reverse()
    })

    return {
      user,
      posts
    }
  },

  head () {
    return {
      title: 'Home ✨'
    }
  }
})
</script>

<style lang="scss" scoped>
#index {
  .br {
    border-radius: 1em;
  }

  .header {
    &-right {
      float: right;
    }
  }
}
</style>
