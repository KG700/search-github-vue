<template>
  <v-container>
    <v-form>
      <v-text-field
        label="Search Github Usernames..."
        prepend-icon="mdi-magnify"
      />
    </v-form>
    <v-card width="280px" class="mx-auto mt-5">
      <v-img :src="user.avatar_url"></v-img>
      <v-card-title>
        <a :href="user.html_url"
          ><h2 class="display-1">{{ user.name }}</h2></a
        >
      </v-card-title>
      <v-card-subtitle>created: {{ user.created_at }}</v-card-subtitle>
    </v-card>
    <v-list-item>
      <v-list-item-content>
        <v-list-item-title v-for="repo in repos" :key="repo.id">{{ repo.name }}</v-list-item-title>
      </v-list-item-content>
    </v-list-item>
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
  props: {
    username: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      user: {},
      repos: {}
    };
  },
  created() {
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
  }
});
</script>
