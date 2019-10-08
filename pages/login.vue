<template>
  <section class="section">
    <div class="container">
      <div class="columns">
        <div class="column is-10 is-offset-1">
          <h2 id="login-welcome-back" class="is-size-2 has-text-centered has-text-primary has-text-weight-bold">
            Welcome back!
          </h2>

          <Notification v-if="error" :message="error" />

          <form method="post" @submit.prevent="login">
            <div class="field">
              <label class="label">Email</label>
              <div class="control">
                <input
                  v-model="email"
                  type="email"
                  class="input"
                  name="email"
                >
              </div>
            </div>
            <div class="field">
              <label class="label">Password</label>
              <div class="control">
                <input
                  v-model="password"
                  type="password"
                  class="input"
                  name="password"
                >
              </div>
            </div>
            <div class="control">
              <button type="submit" class="button is-info is-fullwidth">
                Log In
              </button>
            </div>
          </form>
          <div class="has-text-centered" style="margin-top: 20px">
            <p>
              Don't have an account? <nuxt-link to="/register">
                Register
              </nuxt-link>
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Notification from '~/components/Notification'

export default {
  layout: 'main',
  middleware: 'guest',
  components: {
    Notification
  },

  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },

  methods: {
    async login () {
      try {
        await this.$auth.loginWith('local', {
          data: {
            email: this.email,
            password: this.password
          }
        })

        this.$router.push('/')
      } catch (e) {
        this.error = e.response.data.message
      }
    }
  }
}
</script>

<style>
  #login-welcome-back {
    padding-bottom: 1.2rem;
  }
</style>
