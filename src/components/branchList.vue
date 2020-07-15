<template>
  <v-card v-if="show" width="500px" class="mx-auto mt-5">
    <v-btn class="ma-2" outlined color="black" @click="back"
      ><v-icon dark left>mdi-arrow-left</v-icon>BACK</v-btn
    >
    <v-list>
      <branchItem
        v-for="branch in branches"
        :branch="branch"
        :key="branch.id"
      ></branchItem>
    </v-list>
  </v-card>
</template>

<script lang="ts">
import Vue from "vue";
import branchItem from "@/components/branchItem.vue";
// import repoItem from "@/components/repoItem.vue";

export default Vue.extend({
  name: "branchList",
  components: {
    branchItem
  },
  props: {
    show: Boolean,
    branches: Array
  },
  methods: {
    back: function() {
      this.$emit("back");
    }
  }
});
</script>
