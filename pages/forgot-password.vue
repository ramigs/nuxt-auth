<template>
  <section class="section">
    <div class="container">
      <div class="columns">
        <div class="column is-4 is-offset-4">
          <h2 class="title has-text-centered">Forgot Password</h2>

          <Notification v-if="success" type="success" :message="success" />
          <Notification v-if="error" type="danger" :message="error" />

          <form v-if="!success" method="post" @submit.prevent="forgotPassword">
            <div class="field">
              <label class="label">Email</label>
              <div class="control">
                <input
                  v-model="email"
                  type="email"
                  class="input"
                  name="email"
                />
              </div>
            </div>
            <div class="control">
              <button type="submit" class="button is-dark">
                Email me a reset link
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Notification from '~/components/Notification'

export default {
  middleware: 'guest',
  components: {
    Notification
  },
  data() {
    return {
      email: '',
      success: null,
      error: null
    }
  },
  methods: {
    async forgotPassword() {
      try {
        await this.$axios.post('auth/forgot-password', {
          email: this.email
        })
        this.error = null
        this.success = `A reset password link has been sent to your email account. \
        Please click on the link to complete the password reset.`
      } catch (e) {
        this.error = e.response.data.message[0].messages[0].message
      }
    }
  }
}
</script>
