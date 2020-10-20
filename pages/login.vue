<template>
  <section id="login" class="hero is-light is-fullheight">
    <div class="hero-body">
      <div class="container has-text-centered">
        <div class="card form has-text-left">
          <div class="card-header">
            <p class="card-header-title">
              Zeth's Blog
            </p>

            <a
              class="card-header-icon"
              @click="$router.go(-1)"
            ><b-icon icon="close" />
            </a>
          </div>

          <div class="card-content">
            <b-field label="Email" label-position="inside">
              <b-input
                v-model="state.email"
                type="email"
              />
            </b-field>

            <b-field
              label="Password"
              label-position="inside"
              required
            >
              <b-input
                v-model="state.password"
                password-reveal
                type="password"
              />
            </b-field>

            <b-notification v-show="errorMsg" type="is-danger is-light">
              {{ errorMsg }}
            </b-notification>

            <b-button
              type="is-primary login-btn"
              size="is-medium"
              expanded
              icon-right="login"
              @click="validate"
            >
              Login
            </b-button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script lang="ts">
import { defineComponent, reactive, ref, useContext } from '@nuxtjs/composition-api';

export default defineComponent({
  name: 'login',
  layout: 'empty',
  middleware: 'auth',
  auth: 'guest',

  setup () {
    const { $auth } = useContext();

    const state = reactive({
      email: '',
      password: ''
    });

    const errorMsg = ref('');

    const validate = () => {
      if (!state.email || !state.password) {
        errorMsg.value = 'Please enter an email or password.';
        return;
      }

      // Authenticate if form is fine.
      authenticate();
    };

    const authenticate = () => {
      const data = {
        email: state.email,
        password: state.password
      };

      $auth.loginWith('local', { data })
        .then((res: any) => {
          $auth.setUser(res.data.user);
        }).catch((err) => {
          errorMsg.value = err.response.data.message;
        });
    };

    return {
      state,
      errorMsg,
      validate
    };
  },

  head () {
    return {
      title: 'Login'
    };
  }
});
</script>

<style lang="scss" scoped>
#login {
  background-image: url('https://source.unsplash.com/arwTpnIUHdM/1920x1080');
  background-repeat: no-repeat;
  background-size: cover;

  .form {
    max-width: 35em;
    margin: 0 auto;
    border-radius: .3em 2em 2em 2em;
  }

  .login-btn {
    border-bottom-right-radius: 1em;
    border-bottom-left-radius: 1em;
  }
}
</style>
