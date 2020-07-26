<template>
  <div class="text-center">
    <v-pagination
      :value="reposPage"
      :length="totalPages"
      @input="clickEvent"
    ></v-pagination>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from "vue-property-decorator";

@Component
export default class PageNavigation extends Vue {
  @Prop({ type: Number, default: () => 0 })
  reposPage!: number;
  @Prop({ type: Number, default: () => 0 })
  totalPages!: number;

  clickEvent(page: number) {
    this.$emit("pageClick", page);
  }
}
</script>
