<template>
  <div id="app">
    <div class="logo-box d-flex">
      <img src="./assets/logo.png" alt="" />
    </div>
    <input type="text" v-model="searchText" />
    <button @click="firstFunction(); secondFunction();">cerca</button>
    <div v-if="movies">
      <div v-for="movie in movies.results" :key="movie.id">
         <img :src="ImageCard(movie.poster_path)" alt="">
        {{ movie.title }}
        {{ movie.original_title }}
        {{ movie.overview }}
        <flag :iso="movie.original_language" />
        
        <star-rating :rating="Math.ceil(parseInt(movie.vote_average) / stella)"/>
      </div>
    </div>
    <!-- ricerca serie tv -->
    <div v-if="series">
      <div v-for="serie in series.results" :key="serie.id">
         <img :src="ImageCard(serie.poster_path)" alt="">
        {{ serie.title }}
        {{ serie.original_title }}
        {{ serie.original_language }}
         <star-rating :rating="Math.ceil(parseInt(serie.vote_average) / stella)"/>
        
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import StarRating from 'vue-star-rating'
export default {
  name: "App",
  components: {
     StarRating, 
  },
  data() {
    return {
      searchText: "",
      api_key:'5ad2455a12cd749ceea122cfdf1861d7',
      movies: null,
      series: null,
      stella: 2,
      falgs:['it','ja','en','fr']
      
    };
  },
  methods: {
   firstFunction() {
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=5ad2455a12cd749ceea122cfdf1861d7&query=${this.searchText}`
        )
        .then((resp) => {
          this.movies = resp.data;
          console.log(resp);
        });
    },
    secondFunction() {
      axios
      .get(
        `https://api.themoviedb.org/3/search/tv?api_key=5ad2455a12cd749ceea122cfdf1861d7&query=${this.searchText}`
      )
      .then((resp) => {
         this.series = resp.data;
      });

    },
    ImageCard(name) {
      if(!name){
        return 'https://placeholder.pics/svg/342x513/DEDEDE/555555/Coming%20Soon'
      }
      return `https://image.tmdb.org/t/p/w342/${name}`
    }
  },
  getVote(vote) {
      return Math.ceil(vote / 2)
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
