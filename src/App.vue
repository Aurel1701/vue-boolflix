<template>
  <div id="app">
     <div class="logo-box d-flex">
          <img src="./assets/logo.png" alt="" />
        </div>
    <input type="text" v-model="searchText" />
    <button @click="callApi">cliccami</button>
    <div v-if="movies">
      <div v-for="movie in movies.results" :key="movie.id">
        {{ movie.title }}
        {{ movie.original_title }}
        {{ movie.original_language }}
        {{ movie.vote_average }}
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  components: {},
  data() {
    return {
      searchText: "",
      movies: null,
    };
  },
  methods: {
    callApi() {
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=5ad2455a12cd749ceea122cfdf1861d7&query=${this.searchText}`
        )
        .then((resp) => {
          this.movies = resp.data;
          console.log(resp);
        });
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
