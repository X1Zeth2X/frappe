<template>
  <div id="read" class="post">
    <img :src="post.imageUrl" class="post__img">

    <div
      class="card post__content animate__animated animate__bounceIn"
    >
      <b-loading v-model="loading" :is-full-page="false" />

      <div v-show="!loading" class="card-content">
        <div>
          <span class="is-size-2 title oswald">
            {{ post.title }}
          </span>

          <b-dropdown v-if="$auth.loggedIn" aria-role="list" class="float__right">
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
          {{ post.author.fullName }}
          &middot; {{ prettyDate(post.createdAt) }}
        </div>

        <div>
          <markdown-it-vue-light
            class="md-body post__text"
            :content="content"
          />
        </div>
      </div>
    </div>

    <b-button
      class="topBtn"
      icon-right="chevron-up"
      size="is-large"
      type="is-info"
      outlined

      @click="goTop"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, ref, useContext } from '@nuxtjs/composition-api';
import moment from 'moment';

export default defineComponent({
  name: 'read',

  setup (_, { root }) {
    const [route, router] = [root.$route, root.$router];
    const { $axios } = useContext();
    const loading = ref(true);

    const post = ref({
      id: Number,
      author: Object,
      title: String,
      content: String,
      createdAt: String,
      updatedAt: String
    });

    const content = ref('');

    onMounted(async () => {
      const resp = await $axios.$get(`https://zeth-juno.herokuapp.com/post/${route.params.id}`);
      post.value = resp.post;
      content.value = resp.post.content;

      setTimeout(() => {
        loading.value = false;
      }, 250);
    });

    const deletePost = () => {
      $axios.$delete(`https://zeth-juno.herokuapp.com/post/${route.params.id}`);
      router.replace({ name: 'index' });
    };

    const prettyDate = (date: string) => moment(date).utc().format('MMM do, YYYY');

    const goTop = () => window.scrollTo({ top: 0 });

    return {
      post,
      content,
      loading,

      deletePost,
      prettyDate,
      goTop
    };
  },

  head () {
    return {
      title: 'Read 📖'
    };
  }
});
</script>

<style lang="scss" scoped>
#read {
  .post {
    &__img {
      -webkit-clip-path: polygon(0 0, 100% 0, 100% 92%, 0 100%);
      clip-path: polygon(0 0, 100% 0, 100% 92%, 0 100%);
      height: 70vh;
      width: 100%;
      object-fit: cover;
      position: absolute;
      top: 0px;
    }

    &__content {
      border-radius: 2em;

      max-width: 85rem;
      min-height: 12em;
      margin: 5rem auto;
      padding: 2em 3em 4em;
    }

    &__text {
      font-size: 1.15rem;
      font-family: 'Oxygen', sans-serif;
    }

    &__negmt {
      margin-top: -25em;
    }
  }

  .topBtn {
    position: fixed;
    bottom: 20px;
    right: 20px;
    z-index: 99;
    border-radius: 2em;
  }
}
</style>
