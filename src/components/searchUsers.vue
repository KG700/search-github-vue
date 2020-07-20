<template>
  <v-form @submit.prevent>
    <v-autocomplete
      v-model="username"
      label="Github users"
      placeholder="Search Github Usernames..."
      prepend-icon="mdi-magnify"
      :items="userOptions"
      :loading="isLoading"
      :search-input.sync="search"
      hide-no-data
    >
    </v-autocomplete>
  </v-form>
</template>

<script lang="ts">
import { Component, Vue, Watch } from "vue-property-decorator";
import axios, { AxiosStatic } from "axios";

@Component
export default class SearchUsers extends Vue {
  private users = [];
  private username = null;
  private search = null;
  private isLoading = false;

  @Watch("search")
  searchChange(val) {
    if (this.search === null || this.search === "") {
      this.isLoading = false;
      return;
    }
    console.log(this.isLoading);
    if (this.isLoading) return;

    this.isLoading = true;

    console.log(`https://api.github.com/search/users?per_page=6&q=${val}`)

    axios
      .get(`https://api.github.com/search/users?per_page=6&q=${val}`)
      .then(response => {
        console.log(response.data.items)
        this.users = response.data.items;
        this.isLoading = false;
      });
  }

  @Watch("username")
  selectedUser() {
    this.$emit("selectUser", this.username);
  }

  get userOptions() {
    return this.users.map(user => {
      return user.login;
    });
  }
}
</script>
