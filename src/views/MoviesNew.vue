<template>
  <div class="movies-new">
    <form v-on:submit="createMovie()">
      Title: <input type="text" v-model="title">
      Director: <input type="text" v-model="director">
      Year: <input type="text" v-model="year">
      Plot: <input type="text" v-model="plot">
      <input type="submit" value="Submit">
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      title: "",
      director: "",
      year: "",
      plot: "",
      errors: []
    };
  },
  created: function () {},
  methods: {
    createMovie: function () {
      var params = {
        title: this.title,
        director: this.director,
        year: this.year,
        plot: this.plot,
      };
      axios
        .post("/api/movies", params)
        .then(response => {
          this.$route.push("/movies");
        });
    }
  }
};
</script>