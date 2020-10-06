<template>
  <b-navbar id="navbar" shadow>
    <template slot="brand" class="brand">
      <nuxt-link :to="{ name: 'index' }" class="navbar-item">
        <p class="teko name">
          Zeth<span class="name-colored">.</span>
        </p>
      </nuxt-link>
    </template>

    <template slot="end">
      <b-navbar-item tag="div">
        <div v-if="!$auth.loggedIn" class="buttons">
          <b-button
            tag="nuxt-link"
            type="is-info"
            icon-right="login"
            :to="{ name: 'login' }"
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
    </template>
  </b-navbar>
</template>

<style lang="scss" scoped>
#navbar {
  .brand {
    &-signature {
      padding: .5em;
      height: 4em;
      stroke: #313131;
    }
  }

  .name {
    font-size: 40px;

    &-colored {
      color: red;
    }
  }
}
</style>
