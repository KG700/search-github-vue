<template>
  <v-container style="width: 700px">
    <welcome :show="!showUser"></welcome>
    <searchUsers @selectUser="findUser"></searchUsers>
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
import welcome from "./Welcome.vue";
import searchUsers from "./SearchUsers.vue";
import selectedUser from "./SelectedUser.vue";
import repoList from "./RepoList.vue";
import branchList from "./BranchList.vue";

Vue.prototype.$axios = axios;

declare module "vue/types/vue" {
  interface Vue {
    $axios: AxiosStatic;
  }
}

@Component({
  components: {
    welcome,
    searchUsers,
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

  findUser(user: string) {
    console.log("finding user");
    console.log(user);
    axios.get(`https://api.github.com/users/${user}`).then(response => {
      this.user = response.data;
    });
    axios
      .get(`https://api.github.com/users/${user}/repos?per_page=100`)
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
