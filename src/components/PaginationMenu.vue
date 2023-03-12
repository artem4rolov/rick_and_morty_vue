<template>
  <div class="pagination__wrapper">
    <button class="start">1</button>
    <button>...</button>
    <button class="page">Предыдущая</button>
    <button class="currentPage">Текущая</button>
    <button class="page">Следующая</button>
    <button>...</button>
    <button class="end">42</button>
  </div>
</template>

<script>
export default {
  name: "PaginationMenu",
  props: {
    pagination: Object,
  },
  data() {
    return {
      paginationData: null,
    };
  },
  async mounted() {
    this.paginationData = await this.pagination;
    console.log(this.paginationData.nexPage.split("=")[1]);
    console.log(this.paginationData.prevPage.split("=")[1]);
  },
};
</script>

<style>
.pagination__wrapper {
  display: flex;
  align-items: center;
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
  font-size: 14px;
  cursor: pointer;
}

.page:hover {
  opacity: 0.6;
}

.currentPage {
  font-size: 18px;
  font-weight: 700;
  cursor: pointer;
}

.currentPage:hover {
  opacity: 0.6;
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
