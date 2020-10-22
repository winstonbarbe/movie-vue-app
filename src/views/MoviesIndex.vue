<template>
  <div class="movies-index">
    <h1>Movies</h1>
    <div v-for="movie in movies">
      <h3>{{ movie.title }}</h3>
      <p>{{ movie.director }}</p>
      <p>{{ movie.year }}</p>
      <p>{{ movie.plot }}</p>
      <router-link :to="`/movies/${movie.id}`">More info</router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: []
    };
  },
  created: function () {
    axios.get("/api/movies").then( response => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {
  }
};
</script>