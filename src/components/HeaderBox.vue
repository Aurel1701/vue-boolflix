<template>
  <header class="container-fluid d-flex header">
    <div class="container d-flex">
      <div class="logo-box d-flex">
        <img src="../assets/logo.png" alt="" />
      </div>
      <input
        v-model="keySearch"
        @keyup.enter="searchKeyword"
        type="text"
        class="form-control me-3 border border-danger rounded"
        placeholder="Cerca un film"
        aria-label="Search"
      />
      <button
        @click="searchKeyword"
        type="button"
        class="btn text-light rounded"
      >
        Cerca
      </button>
    </div>
  </header>
</template>


<script>
export default {
  data() {
    return {
      keySearch: "", // creo una variabile per stabilire il valore di quello che uno scrive dentro 
    };
  },
  methods: {
    searchKeyword() {
      this.$emit("searching", this.keySearch); //  farà l'emit
    },
  },
};
</script>

<style>
</style>