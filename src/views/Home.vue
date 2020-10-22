<template>
  <div class="home">
    <h1>Movies</h1>
    <div>
      <h2>Add Movie</h2>
      Title: <input v-model="newMovieTitle" type="text"><br><br>
      Year: <input v-model="newMovieYear" type="text"><br><br>
      Plot: <input v-model="newMoviePlot" type="text"><br><br>
      Director: <input v-model="newMovieDirector" type="text"><br><br>
     <button v-on:click="createMovie()">Add</button>
   </div>

    <div v-for="movie in movies">
      <h3>{{ movie.title }}</h3>
      <h4>Genres:</h4>
      <div v-for="genre in movie.genres">
        <p>{{ genre }}</p>
      </div>
      <p>Year: {{ movie.year }}</p>
      <p>Director: {{ movie.director }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <button v-on:click="showMovie(movie)">More Info</button>
    </div>

    <dialog id="movie-details">
      <form method="dialog">
        <h2>Movie Info</h2>
        {{ currentMovie }}
        <p>Title: <input type="text" v-model="currentMovie.title"></p>
        <p>Year: <input type="text" v-model="currentMovie.year"></p>
        <p>Director: <input type="text" v-model="currentMovie.director"></p>
        <p>Plot: <input type="text" v-model="currentMovie.plot"></p>
        <button v-on:click="updateMovie(currentMovie)">Update</button>
        <button v-on:click="destroyMovie(currentMovie)">delete</button>
        <button>Close</button>
      </form>
    </dialog>
      
    
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      movies: [],
      newMovieDirector: "",
      newMoviePlot: "",
      newMovieTitle: "",
      newMovieYear: "",
      newMovieEnglish: true,
      newMovieGenre: [],
      currentMovie: {}
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/api/movies").then( response => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
    createMovie: function () {
      var params = {
        title: this.newMovieTitle,
        year: this.newMovieYear,
        director: this.newMovieDirector,
        plot: this.newMoviePlot,
        english: this.newMovieEnglish,
        genres: this.newMovieGenre
      };
      axios.post("api/movies", params).then(response => {
        console.log("Success", response.data);
        this.movies.push(response.data);
        this.newMovieDirector = "";
        this.newMovieTitle = "";
        this.newMoviePlot = "";
        this.newMovieYear = "";
        this.newMovieGenre = [];

      }).catch(error => {
        console.log(error.response.data.errors);
      });
      
    },
    showMovie: function (movie) {
      console.log(movie);
      this.currentMovie = movie;
      document.querySelector("#movie-details").showModal();
    },
    updateMovie: function (movie) {
      var params = {
        title: movie.title,
        plot: movie.plot,
        year: movie.year,
        director: movie.director
      };
      axios.patch(`/api/movies/${movie.id}`, params).then( response => {
        console.log("Success", response.data);
      }).catch(error => {
        console.log(error.response.data.errors);
      });
    },
    destroyMovie: function (movie) {
      axios.delete(`/api/movies/${movie.id}`).then(response => {
        console.log("Success", response.data);
        var index = this.movies.indexOf(movie);
        this.movies.splice(index, 1);

      });
    }
  }
};
</script>