<template>
  <v-container>
    <v-card v-if="show" width="500px" class="mx-auto mt-5">
      <v-btn outlined :disabled="reposPage === 0" @click="previousRepoPage"
        ><v-icon dark left>mdi-arrow-left</v-icon>PREVIOUS</v-btn
      >
      <v-btn outlined :disabled="disableNext" @click="nextRepoPage">NEXT<v-icon dark right>mdi-arrow-right</v-icon></v-btn>
      <v-list>
        <v-list-item-group>
          <repoItem
            v-for="repo in displayRepos"
            :repo="repo"
            :user="user"
            :key="repo.id"
            @select="selectEvent"
          ></repoItem>
        </v-list-item-group>
      </v-list>
    </v-card>
  </v-container>
</template>

<script lang="ts">
import Vue from "vue";
import repoItem from "@/components/repoItem.vue";

export default Vue.extend({
  name: "repoList",
  components: {
    repoItem
  },
  props: {
    show: Boolean,
    user: String,
    repos: Array
  },
  data () {
    return {
      reposPage: 0
    };
  },
  computed: {
    displayRepos: function() {
      const firstRepo = this.reposPage * 25;
      const lastRepo = this.reposPage * 25 + 25;
      return this.repos.slice(firstRepo, lastRepo);
    },
    disableNext: function() {
      return this.reposPage === Math.floor(this.repos.length / 25);
    },
  },
  methods: {
    nextRepoPage: function() {
      this.reposPage++;
    },
    previousRepoPage: function() {
      this.reposPage--;
    },
    selectEvent: function(repo: string) {
        this.$emit("select", repo);
    },
  }
});
</script>