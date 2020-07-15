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
import Vue from "vue";

export default Vue.extend({
  name: "branchListItem",
  props: {
    branch: Object
  }
});
</script>
