<template>
  <v-card fixed v-if="show" width="500px" class="mx-auto mt-5">
    <div class="d-flex flex-row">
      <v-avatar size="120" class="ma-3">
        <v-img :src="user.avatar_url"></v-img>
      </v-avatar>
      <div class="d-flex flex-column">
        <v-card-title class="pa-0 mt-5">
          <v-btn x-large text :href="user.html_url">{{ user.name }}</v-btn>
        </v-card-title>
        <v-card-text class="ml-2"
          ><v-icon>mdi-github</v-icon> Joined: {{ formattedDate }}</v-card-text
        >
      </div>
    </div>
  </v-card>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import moment from "moment";

const AppProps = Vue.extend({
  props: {
    show: {
      type: Boolean
    },
    user: {
      type: Object
    }
  }
});

@Component
export default class SelectedUser extends AppProps {
  get formattedDate() {
    return moment(this.user.created_at).format("DD MMM YYYY");
  }
}
</script>
