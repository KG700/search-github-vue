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
import Vue from "vue";
import branchListItem from "@/components/branchListItem.vue";

export default Vue.extend({
  name: "branchList",
  components: {
    branchListItem
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
