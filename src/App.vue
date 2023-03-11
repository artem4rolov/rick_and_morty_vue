<template>
  <div id="app">
    <div v-for="char of characters" :key="char.id">
      <CharCard :char="char" />
    </div>
  </div>
</template>

<script>
import CharCard from "./components/CharCard.vue";

export default {
  name: "App",
  data() {
    return {
      characters: [],
    };
  },
  components: {
    CharCard,
  },
  mounted() {
    this.getCharacters();
  },
  methods: {
    getCharacters() {
      fetch("https://rickandmortyapi.com/api/character")
        .then((res) => res.json())
        .then((data) => (this.characters = data.results))
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
}
</style>
