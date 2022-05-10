<template>
  <div id="app">
    <header class="container-fluid d-flex header">
      <div class="container d-flex">
        <div class="logo-box d-flex">
          <img src="./assets/logo.png" alt="" />
        </div>
        <input
          v-model="keySearch"
          @keyup.enter="searchListMovie" 
          type="text"
          class="form-control mt-3 border rounded"
          placeholder="Cerca un film"
          aria-label="Search"
        />
        <button type="button" @click="movieSearch" class="btn text-light rounded">Cerca</button>
      </div>
    </header>

    <!-- ricerca film -->

    <div>
      <div>
        <h4 class="text-light text-center">Films:</h4>
      </div>

      <div class="d-flex justify-content-center">
         <!-- <cards-box
          v-for="movie in movies"
          :key="movie.id"
          :info="movie"
          :type="'movie'"
        /> -->
        <img id="" :src="``" />
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
      movies: [], // array film  da riempire tramite la chiamata con i film salvati
      api_key: "5ad2455a12cd749ceea122cfdf1861d7",
      keySearch: "",
    };
  },
  mounted() {
     this.movieSearch();
  },
  methods: {
     movieSearch(){
      return axios.get(`https://api.themoviedb.org/3/search/movie?api_key=5ad2455a12cd749ceea122cfdf1861d7&query=matrix`).then((response) => {
        this.movies = response.data.results;       
      });
      
    },

  }
  
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
