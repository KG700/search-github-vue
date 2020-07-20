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
      <v-list-item-subtitle class="ml-4">
        Created: {{ formattedDate
        }}<span v-if="displayBranchInfo" class="d-flex justify-end font-italic"
          >Click to see branches<v-icon dark right
            >mdi-arrow-right</v-icon
          ></span
        >
      </v-list-item-subtitle>
    </v-list-item-content>
  </v-list-item>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import moment from "moment";
import axios, { AxiosStatic } from "axios";

Vue.prototype.$axios = axios;

declare module "vue/types/vue" {
  interface Vue {
    $axios: AxiosStatic;
  }
}

const AppProps = Vue.extend({
  props: {
    repo: {
      type: Object
    },
    user: {
      type: String
    }
  }
});

@Component
export default class RepoListItem extends AppProps {
  displayBranchInfo = false;

  get formattedDate() {
    return moment(this.repo.created_at).format("DD MMM YYYY hh:mm A");
  }

  select() {
    this.$emit("select", this.repo.name);
  }
  branchDisplayShow() {
    this.displayBranchInfo = true;
  }
  branchDisplayHide() {
    this.displayBranchInfo = false;
  }
}
</script>
