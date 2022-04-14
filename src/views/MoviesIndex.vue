<script>
import axios from "axios";

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
      <p>Plot: {{ movie.plot }}</p>
      <button v-on:click="showMovie(movie)">More info</button>
    </div>
  </div>
</template>
