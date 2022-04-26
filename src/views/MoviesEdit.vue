<script>
import axios from "axios";

export default {
  data: function () {
    return {
      editMovieParams: {},
      movie: {},
      errors: [],
    };
  },
  created: function () {
    axios.get("/movies/" + this.$route.params.id + ".json").then((response) => {
      console.log("movies show", response);
      this.movie = response.data;
      this.editMovieParams = this.movie;
    });
  },
  methods: {
    updateMovie: function () {
      console.log("edit movie");

      axios.patch("/movies/" + this.$route.params.id + ".json", this.movie).then((response) => {
        console.log("Hooray! Success!", response.data);
        this.$router.push("/movies");
      });
    },
  },
};
</script>
<template>
  <div class="movies-edit">
    <h1>Make an edit to:</h1>
    <h4>"{{ movie.title }}"</h4>
    <form v-on:submit.prevent="updateMovie()">
      Title:
      <input type="text" v-model="editMovieParams.title" />
      <br />
      Year:
      <input type="text" v-model="editMovieParams.year" />
      <br />
      Plot:
      <input type="text" v-model="editMovieParams.plot" />
      <br />
      Director:
      <input type="text" v-model="editMovieParams.director" />
      <br />
      <br />
      <input type="submit" value="update" />
      <br />
      <br />
      <router-link to="/movies">Back to database</router-link>
    </form>
  </div>
</template>
