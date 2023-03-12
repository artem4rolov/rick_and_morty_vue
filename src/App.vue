<template>
  <div id="app">
    <div v-for="char of characters" :key="char.id">
      <CharCard v-if="characters" :char="char" />
    </div>
    <div v-if="pagination !== null" class="pagination__wrapper">
      <button @click="getCharacters(pagination.startUrl)" class="start">
        1
      </button>
      <button>...</button>
      <button @click="getCharacters(pagination.prevPageUrl)" class="page">
        {{ pagination.prevPageNumber }}
      </button>
      <button class="currentPage">
        {{
          pagination.nexPageNumber - 1 === -1
            ? 42
            : pagination.nexPageNumber - 1
        }}
      </button>
      <button @click="getCharacters(pagination.nexPageUrl)" class="page">
        {{ pagination.nexPageNumber }}
      </button>
      <button>...</button>
      <button @click="getCharacters(pagination.endUrl)" class="end">42</button>
    </div>
  </div>
</template>

<script>
import CharCard from "./components/CharCard.vue";

export default {
  name: "App",
  data() {
    return {
      characters: null,
      pagination: null,
    };
  },
  components: {
    CharCard,
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

.pagination__wrapper {
  position: fixed;
  width: 100vw;
  height: 60px;
  bottom: -1px;
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
