<template>
  <v-card v-if="show" width="500px" class="mx-auto mt-5">
    <v-btn small text class="ma-2" @click="back"
      ><v-icon small dark left>mdi-arrow-left</v-icon>BACK</v-btn
    >
    <div class="text-h5 d-flex justify-center">
      Branches of: {{ selectedRepo }}
    </div>
    <v-list>
      <branchListItem v-for="branch in branches" :key="branch.id">
        {{ branch.name }}</branchListItem
      >
    </v-list>
  </v-card>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import BranchListItem from "./BranchListItem.vue";

@Component({
  components: {
    BranchListItem
  },
  props: {
    show: {
      type: Boolean
    },
    branches: {
      type: Array
    },
    selectedRepo: {
      type: String
    }
  }
})
export default class BranchList extends Vue {
  back() {
    this.$emit("back");
  }
}
</script>
