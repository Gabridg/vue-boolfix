<template>
  <div id="app" class="container">
    <Header @search="startSearch" @key.up="enter"></Header>
    <h2 class="fw-bold">Movies</h2>
    <section class="d-flex flex-wrap" id="movies">
      <ProductionCard v-for="movie in movies" :key="movie.id" :production="movie" />
    </section>

    <h2 class="fw-bold">Series</h2>
    <section class="d-flex flex-wrap" id="series">
      <ProductionCard v-for="serie in series" :key="serie.id" :production="serie" />
    </section>
  </div>
</template>

<script>
import axios from "axios";
import Header from './components/TheHeader.vue';
import ProductionCard from './components/ProductionCard.vue';

export default {
  name: 'App',
  components: {
    Header,
    ProductionCard,
  },
  data() {
    return {
      movies: [],
      series: [],
      api: {
        key: 'd8b1d95de4ff2136d2f7b550cf11c6b9',
        baseUri: 'https://api.themoviedb.org/3',
        language: 'it-IT',
      }
    }
  },
  methods: {
    startSearch(query) {
      if (!query) {
        this.movies = this.series = [];
        return;
      }

      const { key, language } = this.api;

      const config = {
        params: {
          api_key: key,
          language,
          query,
        }
      };

      this.fetchedData('/search/movie', config, "movies");
      this.fetchedData('/search/tv', config, "series");
    },

    fetchedData(endpoint, config, target) {
      axios.get(`${this.api.baseUri}${endpoint}`, config).then((res) => {
        this[target] = res.data.results;
      });
    },
  }
}
</script>

<style lang="scss">
@import'./assets/SCSS/style.scss';

body {
  background-color: #434343;

  h2 {
    color: #fff;
  }
}
</style>
