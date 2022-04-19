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
    });
  },
  methods: {
    updateMovie: function () {
      axios
        .patch("/movie/" + this.movie.id + this.editMovieParams + ".json")
        .then((response) => {
          console.log("movies update", response);
          this.$router.push("/movies");
        })
        .catch((error) => {
          console.log("movies update error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
<template>
  <div class="movies-edit">
    <h1>Edit a movie</h1>
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
      <input type="submit" value="update" />
    </form>
  </div>
</template>
