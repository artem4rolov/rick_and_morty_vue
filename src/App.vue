<template>
  <div id="app">
    <div v-for="char of characters" :key="char.id">
      <CharCard :char="char" />
    </div>
    <PaginationMenu :pagination="pagination" />
  </div>
</template>

<script>
import CharCard from "./components/CharCard.vue";
import PaginationMenu from "./components/PaginationMenu.vue";

export default {
  name: "App",
  data() {
    return {
      characters: [],
      pagination: null,
    };
  },
  components: {
    CharCard,
    PaginationMenu,
  },
  mounted() {
    this.getCharacters();
  },
  methods: {
    async getCharacters() {
      await fetch("https://rickandmortyapi.com/api/character")
        .then((res) => res.json())
        .then((data) => {
          this.characters = data.results;
          this.pagination = data;
        })
        .catch((err) => console.log(err));
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

  display: grid;
  grid-template-columns: repeat(2, 300px);
  align-items: center;
  justify-content: center;
  gap: 30px;
}

@media (max-width: 768px) {
  #app {
    grid-template-columns: repeat(2, 300px);
  }
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
