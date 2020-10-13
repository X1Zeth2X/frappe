<template>
  <div id="composer">
    <section class="hero has-text-centered">
      <div class="hero-body">
        <div class="container">
          <div class="title oswald">
            Compose
          </div>
          <div class="subtitle">
            Create a new blog post.
          </div>
        </div>
      </div>

      <div class="fields">
        <b-field label="Title" label-position="inside">
          <b-input
            v-model="post.title"
          />
        </b-field>

        <b-field label="Image URL" label-position="inside">
          <b-input
            v-model="post.imageUrl"
          />
        </b-field>

        <b-field label="Content" label-position="inside">
          <b-input
            v-model="post.content"
            type="textarea"
          />
        </b-field>

        <b-button
          class="float__left"
          size="is-medium"
          type="is-danger"
          outlined
          @click="$router.go(-1)"
        >
          Cancel
        </b-button>

        <b-button
          class="float__right"
          type="is-success"
          icon-right="check-outline"
          size="is-medium"
          @click="createPost"
        >
          Post
        </b-button>
      </div>
    </section>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, useContext } from '@nuxtjs/composition-api'

export default defineComponent({
  name: 'composer',
  middleware: 'auth',
  auth: true,

  setup (_, { root }) {
    const { $axios } = useContext()

    const post = reactive({
      title: '',
      imageUrl: '',
      content: ''
    })

    const createPost = async () => {
      const resp = await $axios.$post('https://zeth-juno.herokuapp.com/post/create', post)

      if (resp) {
        root.$router.push(`/read/${resp.post.id}`)
      }
    }

    return {
      post,
      createPost
    }
  }
})
</script>

<style lang="scss" scoped>
$breakpoint: 800px;

#composer {
  .fields {
    @media (min-width: $breakpoint) {
      width: 50%;
    }

    width: 90%;
    margin: 0 auto;

    &-btn {
      float: right;
    }
  }
}
</style>
