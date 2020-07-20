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

    <selectedUser :show="showUser" :user="user"></selectedUser>

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
import axios, { AxiosStatic } from "axios";
import selectedUser from "./selectedUser.vue";
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
    selectedUser,
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
  private showUser = false;
  private showRepos = false;
  private showBranches = false;

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
    this.showUser = true;
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

  showUserHandler() {
    if (this.repos.length > 0) {
      this.showUser = true;
    }
  }

  showReposHandler() {
    this.showRepos = true;
    this.showBranches = false;
    this.selectedRepo = "";
  }
}
</script>
