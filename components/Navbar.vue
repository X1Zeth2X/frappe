<template>
  <b-navbar id="navbar" shadow>
    <template slot="brand" class="brand">
      <svg viewBox="0 0 107 76" fill="none" class="brand-signature">
        <path d="M11.1235 36.536C19.9092 28.1594 38.4942 12.4319 42.5491 16.5348C47.6177 21.6633 19.7402 53.973 22.7814 60.1273C25.8226 66.2815 64.3442 34.4846 56.7413 29.8689C49.1383 25.2533 42.0422 36.1935 45.0834 40.6389C48.1246 45.0842 56.2344 52.9473 61.303 44.7417C65.3579 38.1772 62.9926 17.0476 61.303 7.3034L81.0707 75C79.5501 54.6568 74.9883 11.8165 68.906 3.20058C73.8057 11.5772 83.8078 29.9715 84.6187 36.536C85.6325 44.7417 77.5227 9.86767 86.6462 14.9962C95.7697 20.1247 95.2629 38.0746 99.3178 27.3047C103.373 16.5348 107.428 7.3034 99.3178 3.20058C92.8299 -0.0816815 31.736 37.7327 2 57.0501" stroke-width="5" />
      </svg>
    </template>

    <template slot="end">
      <b-navbar-item tag="div">
        <div class="buttons">
          <nuxt-link v-if="!$auth.user" :to="{ name: 'login' }">
            <b-button
              type="is-info"
              icon-right="login"
            >
              Login
            </b-button>
          </nuxt-link>
          <a v-else @click="$auth.logout()">
            <b-button
              type="is-warning"
              icon-right="login"
            >
              Logout
            </b-button>
          </a>
        </div>
      </b-navbar-item>
    </template>
  </b-navbar>
</template>

<style lang="scss" scoped>
#navbar {
  padding: .5em 1em .5em 1em;

  .brand {
    &-signature {
      padding: .5em;
      height: 4em;
      stroke: #313131;
    }
  }
}
</style>
