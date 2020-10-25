<template>
  <div class="movies-index">
    <!-- <h1>Movies</h1>
    Search by name: <input v-model="titleFilter" list="titles" />
    <datalist id="titles">
      <option v-for="movie in movies">{{ movie.title }}</option>
    </datalist>
    <div>
      <button>Sort Alphabetically</button>
    </div>
    <div
      
    >
      <h3>{{ movie.title }}</h3>
      <p>{{ movie.director }}</p>
      <p>{{ movie.year }}</p>
      <p>{{ movie.plot }}</p>
      <router-link :to="`/movies/${movie.id}`">More info</router-link>
    </div> -->

    <div id="fh5co-work-section" class="fh5co-light-grey-section">
      <div class="container">
        <div class="row">
          <div class="col-md-6 col-md-offset-3 text-center fh5co-heading ">
            <h2>Movies</h2>
            <p>
              Watch one.
            </p>
          </div>
        </div>
        <div class="row">
          <div
            v-for="movie in orderBy(
              filterBy(movies, titleFilter, 'title'),
              'title'
            )"
            class="col-md-4 "
          >
            <router-link
              :to="`/movies/${movie.id}`"
              class="item-grid text-center"
            >
              <div class="v-align">
                <div class="v-align-middle">
                  <h3 class="title">{{ movie.title }}</h3>
                  <h5 class="category">{{ movie.director }}</h5>
                  <h5 class="category">{{ movie.year }}</h5>
                  <h5 class="category">{{ movie.plot }}</h5>
                </div>
              </div>
            </router-link>
          </div>
          `
        </div>
      </div>
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
