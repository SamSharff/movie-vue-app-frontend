<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    axios.get("/movies/" + this.$route.params.id + ".json").then((response) => {
      console.log("movies show", response);
      this.movie = response.data;
    });
  },
};
</script>
<template>
  <div class="movies-show">
    <h2>{{ movie.name }}</h2>
    <h2>Title: {{ movie.title }}</h2>
    <p>Year: {{ movie.year }}</p>
    <p>Plot: {{ movie.plot }}</p>
    <p>Director: {{ movie.director }}</p>
    <!-- <button v-on:click="moviesIndex()">Back to movies database</button> -->
    <router-link to="/movies">Back to database</router-link>
  </div>
</template>
