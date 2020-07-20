<template>
  <v-container v-if="show">
    <div class="text-h4 d-flex justify-center font-italic">Welcome to</div>
    <div class="text-h2 d-flex justify-center">
      <v-icon large>mdi-github</v-icon>Github Search
    </div>
    <p class="d-flex justify-center">
      To get started, search for a Github user in the search box below
    </p>
  </v-container>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component({
  props: {
    show: {
      type: Boolean
    }
  }
})
export default class Welcome extends Vue {}
</script>
