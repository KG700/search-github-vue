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

    <v-list-item two-line width="500px">
      <template>
        <v-list-item-content>
          <template v-for="repo in repos">
            <v-list-item-title :key="repo.id">{{ repo.name }}</v-list-item-title>
            <v-list-item-subtitle :key="repo.id">{{ repo.created_at }}</v-list-item-subtitle>
            <v-divider :key="repo.id" class="mt-2 mb-2"></v-divider>
          </template>
        </v-list-item-content>
      </template>
    </v-list-item>



    <!-- <v-list two-line>
          <template v-for="(item, index) in items">
            <v-list-tile-avatar><img :src="item.avatar"></v-list-tile-avatar>
            <v-list-tile-content>
              <v-list-tile-title v-html="item.title"></v-list-tile-title>
              <v-list-tile-sub-title v-html="item.subtitle"></v-list-tile-sub-title>
            </v-list-tile-content>
          </template>
        </v-list> -->

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
