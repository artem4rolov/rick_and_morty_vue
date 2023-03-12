<template>
  <div v-if="paginationData !== null" class="pagination__wrapper">
    <button @click="getCharacters(paginationData.startUrl)" class="start">
      1
    </button>
    <button>...</button>
    <button @click="getCharacters(paginationData.prevPageUrl)" class="page">
      {{ paginationData.prevPageNumber }}
    </button>
    <button class="currentPage">
      {{
        paginationData.nexPageNumber - 1 === -1
          ? 42
          : paginationData.nexPageNumber - 1
      }}
    </button>
    <button @click="getCharacters(paginationData.nexPageUrl)" class="page">
      {{ paginationData.nexPageNumber }}
    </button>
    <button>...</button>
    <button @click="getCharacters(paginationData.endUrl)" class="end">
      42
    </button>
  </div>
</template>

<script>
export default {
  name: "PaginationMenu",
  props: {
    pagination: Object,
    getCharacters: Function,
  },
  data() {
    return {
      paginationData: null,
    };
  },
  async mounted() {
    this.paginationData = await this.pagination;
  },
  watch: {
    pagination: function (val) {
      if (val !== false) {
        this.paginationData = val;
      }
    },
  },
};
</script>

<style>
.pagination__wrapper {
  position: fixed;
  width: 100vw;
  height: 60px;
  bottom: -5px;
  left: 0;
  background: #000000;
  opacity: 0.9;

  display: flex;
  align-items: center;
  text-align: center;
  justify-content: center;
  gap: 15px;
}

button {
  border: none;
  color: #fff;
  background: transparent;
}

.start {
  cursor: pointer;
}

.start:hover {
  opacity: 0.6;
}

.page {
  font-size: 12px;
  cursor: pointer;
}

.page:hover {
  opacity: 0.6;
}

.currentPage {
  font-size: 18px;
  font-weight: 700;
  cursor: pointer;
  margin-bottom: 2px;
}

.end {
  cursor: pointer;
}

.end:hover {
  opacity: 0.6;
}

@media (max-width: 768px) {
  .pagination__wrapper {
    gap: 10px;
  }
}

@media (max-width: 480px) {
  .pagination__wrapper {
    gap: 10px;
  }
}

@media (max-width: 320px) {
  .pagination__wrapper {
    gap: 10px;
  }
}
</style>
