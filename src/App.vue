<template>
  <v-app>
   <HelloComponent />
  </v-app>
</template>

<script lang="ts">
import Vue from "vue";
import HelloComponent from "./components/HelloWorld";

export default Vue.extend({
  name: "App",
  components: {
    HelloComponent
  },
  data: () => ({
    showPassword: false
  })
});
</script>
