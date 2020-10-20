<template>
  <div id="latest">
    <div class="card post-img">
      <div class="card-image">
        <figure class="image">
          <img :src="image" :alt="title" class="post-img">
        </figure>
      </div>
    </div>

    <div class="title mt-5 oswald">
      {{ title }}
    </div>
    <div class="subtitle">
      {{ name }} &middot; {{ prettyDate }}
    </div>

    <b-button
      expanded
      outlined
      type="is-info"
      tag="nuxt-link"
      :to="{ path: `/read/${id}` }"
    >
      Read
    </b-button>
  </div>
</template>

<script lang="ts">
import { defineComponent, useContext } from '@nuxtjs/composition-api';
import moment from 'moment';

export default defineComponent({
  name: 'Post',
  props: {
    id: Number,
    title: String,
    date: String,
    name: String,
    image: String
  },
  setup (props) {
    const { $auth } = useContext();
    const prettyDate = moment.utc(props.date).local().fromNow();

    const isAuthor = () => {
      return $auth.user !== null ? (
        $auth.user.fullName === props.name
      ) : false;
    };

    return {
      prettyDate,
      isAuthor
    };
  }
});
</script>

<style lang="scss" scoped>
#latest {
  .post-img {
    border-radius: 2em;
    object-fit: cover;
    overflow: hidden;
    height: 26em;
  }
}
</style>
