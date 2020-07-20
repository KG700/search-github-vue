<template>
  <v-container>
    <v-form @submit.prevent>
      <v-text-field
        v-model="username"
        label="Search Github Usernames..."
        prepend-icon="mdi-magnify"
        @keyup.enter.prevent="findUser"
      />
    </v-form>
    <p v-show="repos.length === 0" class="mx-auto">
      Search for a Github user in the search box above
    </p>
    <v-card v-if="repos.length > 0" width="200px" class="mx-auto mt-5">
      <v-img :src="user.avatar_url"></v-img>
      <v-card-title>
        <v-btn text :href="user.html_url">{{ user.name }}</v-btn>
      </v-card-title>
      <v-card-subtitle>Joined: {{ formattedDate }}</v-card-subtitle>
    </v-card>

    <repoList
      :show="showRepos"
      :repos="repos"
      :user="user.login"
      @select="getBranches"
    ></repoList>

    <branchList
      :show="showBranches"
      :branches="branches"
      :selectedRepo="selectedRepo"
      @back="showReposHandler"
    ></branchList>
  </v-container>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import moment from "moment";
import axios, { AxiosStatic } from "axios";
import repoList from "./repoList.vue";
import branchList from "./branchList.vue";

Vue.prototype.$axios = axios;

declare module "vue/types/vue" {
  interface Vue {
    $axios: AxiosStatic;
  }
}

@Component({
  components: {
    repoList,
    branchList
  }
})
export default class SearchGithub extends Vue {
  private username = "";
  private user = {};
  private repos = [];
  private selectedRepo = "";
  private branches = [];
  private showRepos = false;
  private showBranches = false;

  get formattedDate() {
    console.log(this.user.created_at);
    console.log(moment(this.user.created_at).format("MM/DD/YYYY"));
    return moment(this.user.created_at).format("DD MMM YYYY");
  }

  findUser() {
    axios
      .get(`https://api.github.com/users/${this.username}`)
      .then(response => {
        this.user = response.data;
      });
    axios
      .get(`https://api.github.com/users/${this.username}/repos?per_page=100`)
      .then(response => {
        this.repos = response.data;
      });
    this.username = "";
    this.showRepos = true;
    this.showBranches = false;
  }

  getBranches(repo: string) {
    this.selectedRepo = repo;
    axios
      .get(
        `https://api.github.com/repos/${this.user.login}/${this.selectedRepo}/branches`
      )
      .then(response => {
        this.branches = response.data;
      });
    this.showRepos = false;
    this.showBranches = true;
  }

  showReposHandler() {
    this.showRepos = true;
    this.showBranches = false;
    this.selectedRepo = "";
  }
}
</script>
