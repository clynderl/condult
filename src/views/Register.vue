<template>
  <div class="auth-page">
    <div class="container page">
      <div class="row">
        <div class="col-md-6 offset-md-3 col-xs-12">
          <h1 class="text-xs-center">Sign Up</h1>
          <p class="text-xs-center">
            <router-link to="/login">Have an account?</router-link>
          </p>
          <validation-errors v-if="validationErrors" :validation-errors="validationErrors"/>
          <form @submit.prevent="onSubmit">
            <fieldset class="form-group">
              <input
                  type="text"
                  placeholder="Username"
                  class="form-control form-control-lg"
                  v-model="username">
            </fieldset>
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
            <button class="btn btn-lg btn-primary pull-xs-right" :disabled="isSubmitting">Sign Up</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ValidationErrors from "../components/ValidationErrors";
import {actionTypes} from "../store/modules/auth";
import {mapState} from "vuex";

export default {
  name: 'McvRegister',
  data() {
    return {
      email: '',
      username: '',
      password: ''
    }
  },
  methods: {
    onSubmit() {
      console.log('Submitted form')
      this.$store.dispatch(actionTypes.register, {
        email: this.email,
        username: this.username,
        password: this.password
      }).then(user => {
        console.log('successfully registered user', user)
        this.$router.push({name: 'globalFeed'})
      })
    },
  },
  computed: {
    ...mapState({
      isSubmitting: state => state.auth.isSubmitting,
      validationErrors: state => state.auth.validationErrors
    }),
    // isSubmitting() {
    //   return this.$store.state.auth.isSubmitting
    // },
    // validationErrors() {
    //   return this.$store.state.auth.validationErrors
    // }
  },
  components: {
    ValidationErrors,
  },
}
</script>

<style scoped>

</style>