<template>
  <v-card v-if="show" width="200px" class="mx-auto mt-5">
    <v-img :src="user.avatar_url"></v-img>
    <v-card-title>
      <v-btn text :href="user.html_url">{{ user.name }}</v-btn>
    </v-card-title>
    <v-card-subtitle>Joined: {{ formattedDate }}</v-card-subtitle>
  </v-card>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import moment from "moment";

@Component({
  props: {
    show: {
      type: Boolean
    },
    user: {
      type: Object
    }
  }
})
export default class SelectedUser extends Vue {
  get formattedDate() {
    console.log(this.user.created_at);
    console.log(moment(this.user.created_at).format("MM/DD/YYYY"));
    return moment(this.user.created_at).format("DD MMM YYYY");
  }
}
</script>
