<template>
  <div id="default">
    <Navbar class="pad-nav" />

    <section class="main-content">
      <nuxt />
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

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Teko:wght@600&Lato&family=Oswald:wght@500&display=swap');

#default {
  .teko {
    font-family: 'Teko', sans-serif;
  }

  .oswald {
    font-family: 'Oswald', sans-serif;
  }

  font-family: 'Lato', sans-serif;

  .pad {
    &-content {
      padding-left: 20px;
      padding-right: 20px;
    }

    &-nav {
      padding-left: 10px;
      padding-right: 10px;
    }
  }

  .mt {
    &-10 {
      margin-top: 10em;
    }
  }
}
</style>
