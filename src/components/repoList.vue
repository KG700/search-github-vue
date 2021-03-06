<template>
  <v-container>
    <v-card v-if="show" width="500px" class="mx-auto mt-5">
      <pageNavigation
        :reposPage="reposPage"
        :totalPages="totalPages"
        @next="nextRepoPage"
        @nextDisabled="disableNext"
        @previous="previousRepoPage"
      ></pageNavigation>
      <div class="text-h5 d-flex justify-center">Repositories</div>
      <v-list>
        <v-list-item-group>
          <repoListItem
            v-for="repo in displayRepos"
            :repo="repo"
            :user="user"
            :key="repo.id"
            @select="selectEvent"
          ></repoListItem>
        </v-list-item-group>
      </v-list>
      <pageNavigation
        :reposPage="reposPage"
        :totalPages="totalPages"
        @next="nextRepoPage"
        @nextDisabled="disableNext"
        @previous="previousRepoPage"
      ></pageNavigation>
    </v-card>
  </v-container>
</template>

<script lang="ts">
import { Component, Vue, Watch } from "vue-property-decorator";
import pageNavigation from "./pageNavigation.vue";
import repoListItem from "./repoListItem.vue";

const AppProps = Vue.extend({
  props: {
    show: {
      type: Boolean
    },
    user: {
      type: String
    },
    repos: {
      type: Array
    }
  }
})

@Component({
  components: {
    repoListItem,
    pageNavigation
  }
})
export default class RepoList extends AppProps {
  private reposPage = 0;

  @Watch("user")
  userChanged() {
    console.log("user changed!");
    this.reposPage = 0;
  }

  get displayRepos() {
    console.log(this.repos);
    const sortedRepos = this.repos.sort((a, b) => {
      return new Date(a.created_at) - new Date(b.created_at)
    });
    const firstRepo = this.reposPage * 25;
    const lastRepo = this.reposPage * 25 + 25;
    return sortedRepos.reverse().slice(firstRepo, lastRepo);
  }

  get disableNext() {
    return this.reposPage === Math.floor(this.repos.length / 25);
  }

  get totalPages() {
    return this.repos.length > 0 ? Math.ceil(this.repos.length / 25) : 1;
  }

  nextRepoPage() {
    this.reposPage++;
  }

  previousRepoPage() {
    this.reposPage--;
  }

  selectEvent(repo: string) {
    this.$emit("select", repo);
  }
}
</script>
