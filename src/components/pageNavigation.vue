<template>
  <div class="d-flex justify-space-between">
    <v-btn small text :disabled="reposPage === 0" @click="previousClickEvent"
      ><v-icon small dark left>mdi-arrow-left</v-icon>PREVIOUS</v-btn
    >
    <span class="font-weight-light"
      >Page {{ reposPage + 1 }} of {{ totalPages }}</span
    >
    <v-btn small text :disabled="disableNext" @click="nextClickEvent"
      >NEXT<v-icon small dark right>mdi-arrow-right</v-icon></v-btn
    >
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

const AppProps = Vue.extend({
  props: {
    reposPage: {
      type: Number
    },
    totalPages: {
      type: Number
    }
  }
});

@Component
export default class PageNavigation extends AppProps {
  get disableNext() {
    return this.reposPage + 1 == this.totalPages;
  }
  nextClickEvent() {
    this.$emit("next");
  }
  previousClickEvent() {
    this.$emit("previous");
  }
}
</script>
