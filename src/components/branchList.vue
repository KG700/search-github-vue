<template>
  <v-card v-if="show" width="500px" class="mx-auto mt-5">
    <v-btn class="ma-2" outlined color="black" @click="back"
      ><v-icon dark left>mdi-arrow-left</v-icon>BACK</v-btn
    >
    <v-list>
      <v-list-item v-for="branch in branches" :key="branch.id">
        <v-list-item-content>
          <v-list-item-title>
            {{ branch.name }}
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>
  </v-card>
</template>

<script lang="ts">
import Vue from "vue";
// import repoItem from "@/components/repoItem.vue";

export default Vue.extend({
  name: "branchList",
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
