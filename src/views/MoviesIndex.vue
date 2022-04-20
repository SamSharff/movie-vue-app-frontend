<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  data: function () {
    return {
      movies: [],
    };
  },
  created: function () {
    axios.get("http://localhost:3000/movies.json").then((response) => {
      this.movies = response.data;
      console.log("All movies", this.movies);
    });
  },
};
</script>

<template>
  <div>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>Title: {{ movie.title }}</h2>
      <p>Year: {{ movie.year }}</p>
      <!-- <router-link v-bind:to="`/movies/${movie.id}`">More info</router-link> -->
      <a :href="`/movies/${movie.id}`">More Info</a>
    </div>
  </div>
</template>
