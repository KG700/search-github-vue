<template>
  <v-card v-if="show" width="500px" class="mx-auto mt-5">
    <v-btn class="ma-2" outlined color="black" @click="back"
      ><v-icon dark left>mdi-arrow-left</v-icon>BACK</v-btn
    >
    <v-list>
      <branchListItem v-for="branch in branches" :key="branch.id">
        {{ branch.name }}</branchListItem
      >
    </v-list>
  </v-card>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import BranchListItem from "./branchListItem.vue";

@Component({
  components: {
    BranchListItem,
  },
  props: {
    show: {
      type: Boolean,
    },
    branches: {
      type: Array,
    },
  }
})

export default class BranchList extends Vue {
  back() {
    this.$emit("back");
  }
};
</script>
