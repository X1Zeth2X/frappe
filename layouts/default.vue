<template>
  <div>
    <Navbar />

    <section class="main-content columns">
      <div class="container column is-10">
        <nuxt />
      </div>
    </section>
  </div>
</template>

<script lang="ts">
import { defineComponent } from '@nuxtjs/composition-api'

import Navbar from '~/components/Navbar.vue'

export default defineComponent({
  components: {
    Navbar
  },
  setup () {
    const items = [
      {
        title: 'Home',
        icon: 'home',
        to: { name: 'index' }
      }
    ]

    return {
      items
    }
  }
})
</script>
