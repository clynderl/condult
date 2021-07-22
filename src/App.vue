<template>
  <div>
    <topbar/>
    <router-view></router-view>
  </div>
</template>
<script>
import Topbar from "./components/Topbar";
import {actionTypes} from "./store/modules/auth";

export default {
  components: {
    Topbar
  },
  mounted() {
    this.$store.dispatch(actionTypes.getCurrentUser)
  }
}
</script>

<style>

</style>
