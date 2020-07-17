<template>
  <v-list-item>
    <v-list-item-content>
      <v-list-item-title>
        <slot></slot>
      </v-list-item-title>
    </v-list-item-content>
  </v-list-item>
</template>

<script lang="ts">
// import Vue from "vue";
import { Component, Vue } from "vue-property-decorator";

@Component({
  props: {
    branch: {
      type: Object
    }
  }
})
export default class BranchListItem extends Vue {}
</script>
