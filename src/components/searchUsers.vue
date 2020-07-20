<template>
<v-form @submit.prevent>
      <!-- <v-text-field
        v-model="username"
        label="Search Github Usernames..."
        prepend-icon="mdi-magnify"
        @keyup.enter.prevent="findUser"
      /> -->
      <v-autocomplete
        v-model="username"
        label="Github users"
        placeholder="Search Github Usernames..."
        prepend-icon="mdi-magnify"
        :items="searchUsers"
      > </v-autocomplete>
    </v-form>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
// import axios, { AxiosStatic } from "axios";

@Component
export default class SearchUsers extends Vue {}
</script>
