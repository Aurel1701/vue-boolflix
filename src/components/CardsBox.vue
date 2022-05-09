<template>
  <div>
    <!-- ricerca film -->
    <div>
      <h4 class="text-light text-center">Films:</h4>
    </div>

    <div class="d-flex justify-content-center">
      <cards-box
        v-for="movie in movies"
        :key="movie.id"
        :info="movie"
        :type="'movie'"
      />
    </div>
  </div>
</template>

<script>
import ResultsBox from "./ResultsBox.vue";
export default {
  ResultsBox,

  props: {
    movies: Array,
    
  },
};
</script>

<style>
</style>