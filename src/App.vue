<template>
  <div id="app">
    <HeaderBox @searching="ricerca" />
    <CardsBox :movies="movies" />
  </div>
</template>

<script>
import HeaderBox from "./components/HeaderBox.vue";
import CardsBox from "./components/CardsBox.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    HeaderBox,
    CardsBox,
  },
  data() {
    return {
      movies: [], // array film  da riempire tramite la chiamata con i film salvati
      api_key: "5ad2455a12cd749ceea122cfdf1861d7",
    };
  },
  methods: {
    searchMov(query) {
      const params = {
        query: query,
        api_key: this.api_key,
      };
      return axios
        .get(`https://api.themoviedb.org/3/movie/{movie_id}?api_key=5ad2455a12cd749ceea122cfdf1861d7&language=en-US`, { params })
        .then((response) => {
          this.movies = response.data.results; 
        });
    },
    ricerca(query){
      this.searchMov(query);
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
