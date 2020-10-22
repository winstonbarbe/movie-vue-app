<template>
  <div class="movies-edit">
    <h1>Edit Movie</h1>
    <form v-on:submit.prevent="updateMovie()">
      Title: <input type="text" v-model="movie.title" /><br />
      Director: <input type="text" v-model="movie.director" /><br />
      Year: <input type="text" v-model="movie.year" /> <br />
      Plot: <input type="text" v-model="movie.plot" /><br />
      <input type="submit" value="Update" />
      <button v-on:click="destroyMovie()">Delete</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      movie: {},
      errors: [],
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {
    updateMovie: function() {
      var params = {
        title: this.movie.title,
        year: this.movie.year,
        plot: this.movie.plot,
        director: this.movie.director,
      };
      axios
        .patch(`/api/movies/${this.$route.params.id}`, params)
        .then((response) => {
          this.$router.push("/movies");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    destroyMovie: function() {
      if (confirm("Confirm!")) {
        axios.delete(`/api/movies/${this.movie.id}`).then((response) => {
          console.log("Success");
          this.$router.push("/movies");
        });
      }
    },
  },
};
</script>
