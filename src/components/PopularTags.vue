<template>
  <div>
    <mcv-loading v-if="isLoading"/>
    <mcv-error-message v-if="error"/>

    <div class="sidebar" v-if="popularTags">
      <p>Popular tags</p>
      <div class="tag-list">
        <router-link
            v-for="popularTag in popularTags"
            :key="popularTag"
            :to="{name: 'tag', params: {slug: popularTag}}"
            class="tag-default tag-pill">
          {{ popularTag }}
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import {mapState} from "vuex";
import {actionTypes} from "../store/modules/popularTags";
import McvLoading from "./Loading";
import McvErrorMessage from "./ErrorMessage";

export default {
  name: 'McvPopularTags',
  computed: {
    ...mapState({
      isLoading: state => state.popularTags.isLoading,
      error: state => state.popularTags.error,
      popularTags: state => state.popularTags.data,
    })
  },
  mounted() {
    this.$store.dispatch(actionTypes.getPopularTags)
  },
  components: {
    McvLoading,
    McvErrorMessage
  }
}
</script>

<style scoped>

</style>