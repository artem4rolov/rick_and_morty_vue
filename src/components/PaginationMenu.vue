<template>
  <div class="pagination__wrapper"></div>
</template>

<script>
export default {
  name: "PaginationMenu",
  props: ["pagination"],
  mounted() {
    this.getPaginationData();
  },
  methods: {
    getPaginationData() {
      if (this.pagination) {
        console.log(this.pagination);
      }
    },
  },
};
</script>

<style></style>
