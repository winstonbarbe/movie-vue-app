<template>
  <div class="movies-index">
    <h1>Movies</h1>
    Search by name: <input v-model="titleFilter" list="titles" />
    <datalist id="titles">
      <option v-for="movie in movies">{{ movie.title }}</option>
    </datalist>
    <div>
      <button>Sort Alphabetically</button>
    </div>
    <div
      v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), 'title')"
    >
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
import Vue2Filters from "vue2-filters";
export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      movies: [],
      titleFilter: "",
    };
  },
  created: function() {
    axios.get("/api/movies").then((response) => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {},
};
</script>
