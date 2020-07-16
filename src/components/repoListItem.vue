<template>
  <v-list-item
    @click="select"
    @mouseover="branchDisplayShow"
    @mouseleave="branchDisplayHide"
  >
    <v-list-item-content>
      <v-list-item-title>
        <v-btn text :href="repo.html_url">{{ repo.name }}</v-btn>
      </v-list-item-title>
      <v-list-item-subtitle>
        {{ repo.created_at
        }}<span v-if="displayBranchInfo" class="d-flex justify-end"
          >Branches -> <v-icon dark right>mdi-arrow-right</v-icon></span
        >
      </v-list-item-subtitle>
    </v-list-item-content>
  </v-list-item>
</template>

<script lang="ts">
import Vue from "vue";
import axios, { AxiosStatic } from "axios";

Vue.prototype.$axios = axios;

declare module "vue/types/vue" {
  interface Vue {
    $axios: AxiosStatic;
  }
}

export default Vue.extend({
  name: "repoListItem",
  props: {
    repo: Object,
    user: String
  },
  data: function() {
    return {
      displayBranchInfo: false
    };
  },
  methods: {
    select: function() {
      this.$emit("select", this.repo.name);
    },
    branchDisplayShow: function() {
      console.log("mouseover")
      this.displayBranchInfo = true;
    },
    branchDisplayHide: function() {
      console.log("mouseleave")
      this.displayBranchInfo = false;
    }
  }
});
</script>
