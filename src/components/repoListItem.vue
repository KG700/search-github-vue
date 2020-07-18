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
          >Branches -><v-icon dark right>mdi-arrow-right</v-icon></span
        >
      </v-list-item-subtitle>
    </v-list-item-content>
  </v-list-item>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import axios, { AxiosStatic } from "axios";

Vue.prototype.$axios = axios;

declare module "vue/types/vue" {
  interface Vue {
    $axios: AxiosStatic;
  }
}

@Component({
  props: {
    repo: {
      type: Object
    },
    user: {
      type: String
    }
  }
})
export default class RepoListItem extends Vue {
  displayBranchInfo = false;

  select() {
    this.$emit("select", this.repo.name);
  }
  branchDisplayShow() {
    console.log("mouseover")
    this.displayBranchInfo = true;
  }
  branchDisplayHide() {
    console.log("mouseleave")
    this.displayBranchInfo = false;
  }
};
</script>
