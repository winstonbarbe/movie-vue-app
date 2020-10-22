<template>
  <div class="movies-show">
    <h2>Title: {{ movie.title }}</h2>
    <p>Director: {{ movie.director }}</p>
    <p>Year: {{ movie.year }}</p>
    <p>Plot: {{ movie.plot }}</p>
    <router-link :to="`/movies/${movie.id}/edit`">Edit</router-link>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      movie: [],
      errors: [],
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {},
};
</script>
