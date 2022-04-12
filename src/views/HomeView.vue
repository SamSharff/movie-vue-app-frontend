<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Movies! Movies! Movies!",
      movies: [],
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("http://localhost:3000/movies.json").then((response) => {
        this.movies = response.data;
        console.log("All movies", this.movies);
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>Title: {{ movie.title }}</h2>
      <p>Year: {{ movie.year }}</p>
      <p>Plot: {{ movie.plot }}</p>
      -->
    </div>
  </div>
</template>

<style></style>
