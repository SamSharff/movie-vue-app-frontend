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
  methods: {
    destroyMovie: function (movie) {
      axios.delete("/movies/" + movie.id + ".json").then((response) => {
        console.log("Destroying movie", response);
        this.$router.push("/movie");
      });
    },
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

    <router-link v-bind:to="`/movies/${movie.id}/edit`">Edit movie</router-link>
    <br />
    <router-link to="/movies">Back to database</router-link>
    <br />
    <button v-on:click="destroyMovie(movie)">Delete movie</button>
  </div>
</template>
