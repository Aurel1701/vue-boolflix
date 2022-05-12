<template>
  <div id="app">
    <div class="header">
      <div class="logo-box">
        <img src="./assets/logo.png" alt="" />
      </div>
      <div class="navbar d-flex ms-5 mt-2">
        <ul class="list-unstyled">
          <li class="px-3">
            <a href="#">Home</a>
          </li>
          <li class="px-3">
            <a href="#">Film</a>
          </li>
          <li class="px-3">
            <a href="#">Serie Tv</a>
          </li>
          <li class="px-3">
            <a href="#">Nuovi e popolari</a>
          </li>
          <li class="px-3">
            <a href="#">La mia lista</a>
          </li>
        </ul>
      </div>
      <div class="input">
        <input type="text" v-model="searchText" />
        <button
          @click="
            firstFunction();
            secondFunction();
          "
        >
          cerca
        </button>
      </div>
    </div>

    <!-- box cards -->
    <div class="vuoto">
      <div class="flex-card" v-if="movies">
        <div class="card-box" v-for="movie in movies.results" :key="movie.id">
          <div class="card-movie">
            <img :src="ImageCard(movie.poster_path)" alt="" />
           <span class="title">{{ movie.title }}</span>
            <span class="original-title">{{movie.original_title }}</span>
           <span class="language"><flag :iso="movie.original_language" /> </span>
            <span class="stars"> <star-rating 
              :rating="Math.ceil(parseInt(movie.vote_average) / stella)"
            /> </span>
          </div>
        </div>
      </div>
      <!-- ricerca serie tv -->
      <div class="flex-card" v-if="series">
        <div class="card-box " v-for="serie in series.results" :key="serie.id">
          <div class="card-serie card-movie">
            <img :src="ImageCard(serie.poster_path)" alt="" />
            <span class="title">{{ serie.title }}</span>
            <span class="original-title">{{ serie.original_title }}</span>
            <span class="language">{{ serie.original_language }}</span>
            <star-rating class="stars"
              :rating="Math.ceil(parseInt(serie.vote_average) / stella)"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import StarRating from "vue-star-rating";
export default {
  name: "App",
  components: {
    StarRating,
  },
  data() {
    return {
      searchText: "",
      api_key: "5ad2455a12cd749ceea122cfdf1861d7",
      movies: null,
      series: null,
      stella: 2,
      falgs: ["it", "ja", "en", "fr"],
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
      if (!name) {
        return "https://placeholder.pics/svg/342x513/DEDEDE/555555/Coming%20Soon";
      }
      return `https://image.tmdb.org/t/p/w342/${name}`;
    },
  },
  getVote(vote) {
    return Math.ceil(vote / 2);
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

.header {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  height: 150px;
  background-color: rgba(0, 0, 2, 1);
  .list-unstyled {
    display: flex;
    justify-content: center;
    align-items: center;
    list-style: none;
  }

  li {
    &:hover {
      font-weight: bold;
      font-size: 18px;
    }

    a {
      text-decoration: none;
      color: lightgray;
      padding: 10px;
    }
  }
  .input-group {
    button {
      background-color: blue;
    }
  }
  .card-box {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: red;
  } 
}
body{
  background: #000;
}
input{
  background:white;
}
button{
  background:lightgray
}
.input{
  display: flex;
  justify-content: center;
  align-items: center;
}
.flex-card {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
}
.card-box {
    width: 33%;
}
.stars {
    align-items: center;
    justify-content: center;
    position: absolute;
    opacity:0;
    display:flex;
    pointer-events: none;
}
.card-movie {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-flow: column;
    
}
.title{
  color: white;
  opacity:0;
  position: absolute;
  margin-top: 80px;
  pointer-events: none;
}
img:hover{
  opacity:0.4;
}
img:hover  ~ .stars {
  opacity:1;
  transition:0.5s;
}
img:hover ~ .title{
  opacity:1;
  transition:0.5s;
}



</style>
