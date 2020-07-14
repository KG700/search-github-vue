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
    <v-card v-if="repos.length > 0" width="280px" class="mx-auto mt-5">
      <v-img :src="user.avatar_url"></v-img>
      <v-card-title>
        <a :href="user.html_url"
          ><h2 class="display-1">{{ user.name }}</h2></a
        >
      </v-card-title>
      <v-card-subtitle>joined: {{ user.created_at }}</v-card-subtitle>
    </v-card>

    <!-- <v-card v-if="repos.length > 0" width="550px" class="mx-auto mt-6"> -->
      <v-list-item two-line v-if="repos.length > 0">
        <template>
          <v-list-item-content>
            <template v-for="repo in repos">
              <v-card :key="repo.id" class="mt-2 mb-2" @click="getBranches(repo.name)">
                <v-list-item-title :key="repo.id"
                  ><a :href="repo.html_url">{{ repo.name }}</a></v-list-item-title
                >
                <v-list-item-subtitle :key="repo.id"
                  >created: {{ repo.created_at }}</v-list-item-subtitle
                >
                <!-- <v-divider :key="repo.id" class="mt-2 mb-2"></v-divider> -->
              </v-card>
            </template>
          </v-list-item-content>
        </template>
      </v-list-item>
    <!-- </v-card> -->
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
      branches: []
    };
  },
  // calculated: {
  //   usersFound: function() {

  //   },
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
    },
    selectARepo: function(repo: string) {
      console.log("repo selected");
      this.selectedRepo = repo;
    },
    getBranches: function(repo: string) {
      console.log(`https://api.github.com/repos/${this.user.login}/${repo}/branches`)
      axios
        .get(`https://api.github.com/repos/${this.user.login}/${repo}/branches`)
        .then(response => {
          this.branches = response.data;
        });
    }
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
