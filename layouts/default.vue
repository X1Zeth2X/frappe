<template>
  <div id="default">
    <Navbar />

    <section class="main-content">
      <nuxt />
    </section>
  </div>
</template>

<script lang="ts">
import { defineComponent } from '@nuxtjs/composition-api';

import Navbar from '~/components/Navbar.vue';

export default defineComponent({
  transition: 'animate__animated animate__slideIn',
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
    ];

    return {
      items
    };
  }
});
</script>

<style lang="scss">
#default {
  .teko {
    font-family: 'Teko', sans-serif;
  }

  .oswald {
    font-family: 'Oswald', sans-serif;
  }

  font-family: 'Lato', sans-serif;

  .float {
    &__left {
      float: left;
    }

    &__right {
      float: right;
    }
  }

  .mt {
    &-10 {
      margin-top: 10em;
    }
  }
}
</style>
