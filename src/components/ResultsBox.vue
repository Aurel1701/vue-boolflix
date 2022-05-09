<template>
  <!-- se la img ha valore === null stampa questa img -->
  <img
    class="not-found"
    id="show"
    v-if="info.poster_path === null"
    src="https://unsplash.it/200/300?image=876"
    alt="NotAvaible"
  />

  <!-- se l'immagine esiste stampala -->
  <img
    id="show"
    v-else
    :src="`/pB8BM7pdSp6B6Ih7QZ4DrQ3PmJK.jpg${info.poster_path}`"
  />

  
</template>

<script>
export default {
  props: {
    info: Object,
  },
};
</script>

<style>
</style>