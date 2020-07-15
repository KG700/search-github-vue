<template>
  <v-container>
      <v-card v-if="show" width="500px" class="mx-auto mt-5">
      <v-btn outlined :disabled="reposPage === 0" @click="previousRepoPage"
        ><v-icon dark left>mdi-arrow-left</v-icon>PREVIOUS</v-btn
      >
      <v-btn outlined :disabled="disableNext" @click="nextRepoPage">NEXT<v-icon dark right>mdi-arrow-right</v-icon></v-btn>
      <v-list>
        <v-list-item-group>
          <v-list-item
            v-for="repo in displayRepos"
            :key="repo.id"
            @click="getBranches(repo.name)"
          >
            <v-list-item-content>
              <v-list-item-title>
                <v-btn text :href="repo.html_url">{{ repo.name }}</v-btn>
              </v-list-item-title>
              <v-list-item-subtitle>
                {{ repo.created_at }}
              </v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-card>
  </v-container>
</template>



<script lang="ts">
import Vue from "vue";
// import axios, { AxiosStatic } from "axios";

// Vue.prototype.$axios = axios;

// declare module "vue/types/vue" {
//   interface Vue {
//     $axios: AxiosStatic;
//   }
// }

export default Vue.extend({
  name: "repoList",
  props: {
    show: Boolean,
    repos: Array
  },
  data () {
    return {
      reposPage: 0
    };
  },
  computed: {
    displayRepos: function() {
      const firstRepo = this.reposPage * 25;
      const lastRepo = this.reposPage * 25 + 25;
      return this.repos.slice(firstRepo, lastRepo);
    },
    disableNext: function() {
      return this.reposPage === Math.floor(this.repos.length / 25);
    },
  },
  methods: {
    nextRepoPage: function() {
      this.reposPage++;
    },
    previousRepoPage: function() {
      this.reposPage--;
    }
  }
});
</script>