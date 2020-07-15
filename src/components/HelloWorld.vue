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
    <!-- <v-btn type="button" @click="findUser">FIND</v-btn> -->
    <p v-if="repos.length === 0" class="mx-auto">
      Search for a Github user in the search box above
    </p>
    <v-card v-if="repos.length > 0" width="200px" class="mx-auto mt-5">
      <v-img :src="user.avatar_url"></v-img>
      <v-card-title>
        <v-btn text :href="user.html_url">{{ user.name }}</v-btn>
      </v-card-title>
      <v-card-subtitle>joined: {{ user.created_at }}</v-card-subtitle>
    </v-card>

    <!-- <v-card v-if="repos.length > 0" width="550px" class="mx-auto mt-6"> -->
    <v-card v-if="showRepos" width="500px" class="mx-auto mt-5">
      <v-btn outlined><v-icon dark left>mdi-arrow-left</v-icon>PREVIOUS</v-btn>
      <v-btn outlined >NEXT<v-icon dark right>mdi-arrow-right</v-icon></v-btn>
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

    <v-card v-if="showBranches" width="500px" class="mx-auto mt-5">
      <!-- <v-bth class="ma-2" outlined color="indigo" @click="showReposHandler"
        >BACK</v-bth
      > -->
      <v-btn class="ma-2" outlined color="black" @click="showReposHandler"><v-icon dark left>mdi-arrow-left</v-icon>BACK</v-btn>
      <v-list>
        <!-- <v-list-item-group> -->
          <v-list-item v-for="branch in branches" :key="branch.id">
            <v-list-item-content>
              <v-list-item-title>
                {{ branch.name }}
              </v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        <!-- </v-list-item-group> -->
      </v-list>
    </v-card>

  </v-container>
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
  name: "HelloWorld",
  // props: {
  //   username: {
  //     type: String,
  //     required: true
  //   }
  // },
  data() {
    return {
      username: "",
      user: {},
      repos: [],
      selectedRepo: "",
      branches: [],
      showRepos: false,
      showBranches: false,
      reposPage: 0
    };
  },
  computed: {
    displayRepos: function() {
      const firstRepo = this.reposPage * 25
      const lastRepo = (this.reposPage * 25) + 25
      return this.repos.slice(firstRepo,lastRepo);
    },
  },
  methods: {
    findUser: function() {
      axios
        .get(`https://api.github.com/users/${this.username}`)
        .then(response => {
          this.user = response.data;
        });
      axios
        .get(`https://api.github.com/users/${this.username}/repos`)
        .then(response => {
          this.repos = response.data;
        });
      this.username = "";
      this.showRepos = true;
      this.showBranches = false;
    },
    getBranches: function(repo: string) {
      this.selectedRepo = repo;
      axios
        .get(`https://api.github.com/repos/${this.user.login}/${repo}/branches`)
        .then(response => {
          this.branches = response.data;
        });
      this.showRepos = false;
      this.showBranches = true;
    },
    showReposHandler: function() {
      this.showRepos = true;
      this.showBranches = false;
      this.selectedRepo = "";
    },
  }
  // created() {
  //   axios
  //     .get(`https://api.github.com/users/${this.username}`)
  //     .then(response => {
  //       this.user = response.data;
  //     });
  //   axios
  //     .get(`https://api.github.com/users/${this.username}/repos`)
  //     .then(response => {
  //       this.repos = response.data;
  //     });
  // }
});
</script>
