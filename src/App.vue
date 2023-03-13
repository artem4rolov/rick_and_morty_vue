<template>
  <div id="app">
    <div v-for="char of characters" :key="char.id">
      <CharCard v-if="characters" :char="char" />
    </div>
    <LoadingSpinner v-if="loading" alt="" />
    <PaginationMenu
      v-if="!loading"
      v-bind:pagination="pagination"
      v-bind:getCharacters="getCharacters"
    />
  </div>
</template>

<script>
import CharCard from "./components/CharCard.vue";
import PaginationMenu from "./components/PaginationMenu.vue";
import LoadingSpinner from "./components/LoadingSpinner.vue";

export default {
  name: "App",
  data() {
    return {
      characters: null,
      pagination: null,
      loading: true,
    };
  },
  components: {
    CharCard,
    PaginationMenu,
    LoadingSpinner,
  },
  mounted() {
    this.getCharacters();
  },
  methods: {
    async getCharacters(page_url) {
      page_url = page_url || "https://rickandmortyapi.com/api/character";

      await fetch(page_url)
        .then((res) => res.json())
        .then((data) => {
          this.characters = data.results;
          this.makePagination(data.info);
          this.loading = false;
        })
        .catch((err) => console.log(err));
    },
    makePagination(data) {
      // объект пагинации со страницами
      let pagination = {
        startUrl: "https://rickandmortyapi.com/api/character",
        endUrl: "https://rickandmortyapi.com/api/character?page=42",
        currentPageUrl: data,
        currentPageNumber: data,
        nexPageUrl: data.next ? data.next : null,
        nexPageNumber: data.next ? data.next.split("=")[1] : null,
        prevPageUrl: data.prev ? data.prev : null,
        prevPageNumber: data.prev ? data.prev.split("=")[1] : null,
      };

      this.pagination = pagination;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto+Condensed:wght@400;700&display=swap");
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-family: "Roboto Condensed", sans-serif;
  margin-bottom: 100px;

  display: grid;
  grid-template-columns: repeat(2, 300px);
  align-items: center;
  justify-content: center;
  gap: 30px;
}

.lds-spinner {
  margin: 0 auto;
  top: 170px;
}

.pagination__wrapper {
  position: fixed;
  width: 100vw;
  height: 60px;
  bottom: -10px;
  left: 0;
  background: #000000;
  opacity: 0.9;
}

@media (max-width: 768px) {
  #app {
    grid-template-columns: repeat(1, 300px);
  }
}

@media (max-width: 480px) {
  #app {
    grid-template-columns: repeat(1, 300px);
  }
}

@media (max-width: 320px) {
  #app {
    grid-template-columns: repeat(1, 300px);
  }
}
</style>
