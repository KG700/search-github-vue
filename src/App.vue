<template>
  <v-app>
   <searchGithub />
  </v-app>
</template>

<script lang="ts">
import Vue from "vue";
import searchGithub from "@/components/searchGithub.vue";

export default Vue.extend({
  name: "App",
  components: {
    searchGithub
  },
  data: () => ({
    showPassword: false
  })
});
</script>
