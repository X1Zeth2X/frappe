<template>
  <section class="section">
    {{ content }}
    {{ $auth.user }}
    {{ $auth.loggedIn }}

    <div style="background-color: black;" />
    <div style="margin-top: 100em">
      ex
    </div>
  </section>
</template>

<script lang="ts">
import { defineComponent, ref } from '@nuxtjs/composition-api'

import Card from '~/components/Card.vue'

export default defineComponent({
  name: 'Index',
  components: {
    Card
  },

  setup () {
    const content = ref('Lorem Ipsum')

    return {
      content
    }
  },

  head () {
    return {
      title: 'Home ✨'
    }
  }
})
</script>
