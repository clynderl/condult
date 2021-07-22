<template>
  <div class="auth-page">
    <div class="container page">
      <div class="row">
        <div class="col-md-6 offset-md-3 col-xs-12">
          <h1 class="text-xs-center">Sign in</h1>
          <p class="text-xs-center">
            <router-link to="/register">Need an account?</router-link>
          </p>
          <validation-errors v-if="validationErrors" :validation-errors="validationErrors"/>
          <form @submit.prevent="onSubmit">
            <fieldset class="form-group">
              <input
                  type="text"
                  placeholder="Email"
                  class="form-control form-control-lg"
                  v-model="email">
            </fieldset>
            <fieldset class="form-group">
              <input
                  type="password"
                  placeholder="Password"
                  class="form-control form-control-lg"
                  v-model="password">
            </fieldset>
            <button class="btn btn-lg btn-primary pull-xs-right" :disabled="isSubmitting">Sign In</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {mapState} from 'vuex'
import ValidationErrors from "../components/ValidationErrors";
import {actionTypes} from "../store/modules/auth";

export default {
  name: 'McvLogin',
  data() {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    onSubmit() {
      this.$store.dispatch(actionTypes.login, {
        email: this.email,
        password: this.password
      }).then(() => {
        this.$router.push({name: 'globalFeed'})
      })
    },
  },
  // computed: {
  //   isSubmitting() {
  //     return this.$store.state.auth.isSubmitting
  //   },
  //   validationErrors() {
  //     return this.$store.state.auth.validationErrors
  //   },
  // },
  computed: {
    ...mapState({
      isSubmitting: state => state.auth.isSubmitting,
      validationErrors: state => state.auth.validationErrors
    })
  },
  components: {
    ValidationErrors
  }
}
</script>

<style scoped>

</style>