<template>
  <nav class="navbar navbar-light">
    <div class="container">
      <router-link class="navbar-brand" :to="{name: 'globalFeed'}">Medium Clone</router-link>
      <ul class="nav navbar-nav pull-xs-right">
        <li class="nav-item">
          <router-link class="nav-link" :to="{name:'globalFeed'}">Home</router-link>
        </li>
        <template v-if="isLoggedIn">
          <li class="nav-item">
            <router-link class="nav-link" :to="{name:'createArticle'}">
              <i class="ion-compose"/> &nbsp; New Article
            </router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" :to="{name:'settings'}">
              <i class="ion-gear-a"/> &nbsp; Settings
            </router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" :to="{name: 'userProfile', params: {slug: currentUser.username}}">
              <img :src="currentUser.image" class="user-pic" alt="">&nbsp;{{ currentUser.username }}
            </router-link>
          </li>
        </template>
        <template v-if="isAnonymous">
          <li class="nav-item">
            <router-link class="nav-link" :to="{name:'login'}">
              Sign In
            </router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" :to="{name:'register'}">
              Sign Up
            </router-link>
          </li>
        </template>
      </ul>
    </div>
  </nav>
</template>

<script>
import {mapState, mapGetters} from "vuex";
import {getterTypes} from "../store/modules/auth";

export default {
  name: 'mcvTopbar',
  computed: {
    ...mapState({
      // currentUser: state => state.auth.currentUser,
      // isLoggedIn: state => state.auth.isLoggedIn
    }),
    // currentUser() {
    //   return this.$store.getters[getterTypes.currentUser]
    // },
    // isLoggedIn() {
    //   return this.$store.getters[getterTypes.isLoggedIn]
    // },
    // isAnonymous() {
    //   return this.$store.getters[getterTypes.isAnonymous]
    // }
    ...mapGetters({
      currentUser: getterTypes.currentUser,
      isLoggedIn: getterTypes.isLoggedIn,
      isAnonymous: getterTypes.isAnonymous
    })
  },
}
</script>

<style scoped>

</style>