<template>
  <v-container>
    <v-form>
      <v-text-field
        label="Search Github Usernames..."
        prepend-icon="mdi-magnify"
      />
    </v-form>
    <v-card class="mx-auto mt-5">
      <v-img src="https://via.placeholder.com/200"></v-img>
      <v-card-title>
        <a href="https://github.com/KG700"><h2 class="display-1">KG700</h2></a>
      </v-card-title>
      <v-card-subtitle>created: 1 Jan 2019</v-card-subtitle>
    </v-card>
  </v-container>
</template>

<script lang="ts">
import Vue from "vue";
import axios, { AxiosStatic } from 'axios';

Vue.prototype.$axios = axios;

declare module 'vue/types/vue' {
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
  data () {
    return {
      user: {}
    }
  },
  created () {
    axios.get(`https://api.github.com/users/${this.username}`)
      .then(response => {
        console.log(response.data)
      })
  }

});
</script>
