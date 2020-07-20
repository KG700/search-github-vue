<template>
    <div class="d-flex justify-space-between">
        <v-btn small text :disabled="reposPage === 0" @click="previousRepoPage"
          ><v-icon small dark left>mdi-arrow-left</v-icon>PREVIOUS</v-btn
        >
    <span class="font-weight-light"
      >Page {{ reposPage + 1 }} of {{ totalPages }}</span
        <v-btn small text :disabled="disableNext" @click="nextRepoPage"
          >NEXT<v-icon small dark right>mdi-arrow-right</v-icon></v-btn
        >
      </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component({
    props: {
    }
})
export default class PageNavigation extends Vue {}
</script>
