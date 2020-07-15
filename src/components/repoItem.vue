<template>
  <v-list-item @click="getBranches(repo.name)">
    <v-list-item-content>
      <v-list-item-title>
        <v-btn text :href="repo.html_url">{{ repo.name }}</v-btn>
      </v-list-item-title>
      <v-list-item-subtitle>
        {{ repo.created_at }}
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
  name: "repoItem",
  props: {
    repo: Array,
    user: String
  },
  data () {
    return {
      branches: []
    };
  },
  methods: {
    getBranches: function(repo: string) {
      //   this.selectedRepo = repo;
      console.log(`https://api.github.com/repos/${this.user}/${repo}/branches`)
      axios
        .get(`https://api.github.com/repos/${this.user}/${repo}/branches`)
        .then(response => {
          this.branches = response.data;
        });
      //   this.showRepos = false;
      //   this.showBranches = true;
    },
  }
});
</script>