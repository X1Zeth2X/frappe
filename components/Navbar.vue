<template>
  <nav
    id="navbar"
    class="navbar is-dark"
  >
    <div class="container">
      <div class="navbar-brand">
        <nuxt-link :to="{ name: 'index' }" class="navbar-item">
          <p class="teko name">
            Zeth<span class="name-colored">.</span>
          </p>
        </nuxt-link>
      </div>

      <div class="navbar-menu">
        <div class="navbar-end">
          <b-navbar-item @click="open('https://www.linkedin.com/in/zeth-leonardo/')">
            <b-icon icon="linkedin" />
          </b-navbar-item>

          <b-navbar-item @click="open('https://github.com/X1Zeth2X')">
            <b-icon icon="github" />
          </b-navbar-item>

          <b-navbar-item tag="div">
            <div v-if="!$auth.loggedIn" class="buttons">
              <b-button
                tag="nuxt-link"
                type="is-info"
                icon-right="login"
                :to="{ name: 'login' }"
                rounded
              >
                Login
              </b-button>
            </div>

            <div v-else class="buttons">
              <b-button
                tag="nuxt-link"
                icon-right="pen"
                :to="{ name: 'composer' }"
              />

              <b-button
                type="is-warning is-dark"
                icon-right="logout-variant"

                @click="$auth.logout()"
              >
                Logout
              </b-button>
            </div>
          </b-navbar-item>
        </div>
      </div>
    </div>
  </nav>
</template>

<script lang="ts">
import { defineComponent } from '@nuxtjs/composition-api'

export default defineComponent({
  name: 'Navbar',
  setup () {
    const open = (link: string) => window.open(link)

    return {
      open
    }
  }
})
</script>

<style lang="scss" scoped>
#navbar {
  .name {
    font-size: 35px;

    &-colored {
      color: red;
    }
  }
}
</style>
