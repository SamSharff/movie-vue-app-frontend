<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newMovieParams: { plot: "" },
      error: [],
    };
  },
  methods: {
    createMovie: function () {
      console.log("Creating your movie!");

      axios
        .post("http://localhost:3000/movies.json", this.newMovieParams)
        .then((response) => {
          console.log("Sucess!", response.data);
          this.$router.push("/movies");
        })
        .catch((error) => {
          console.log("error creating your photo", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
<template>
  <div class="movies-new">
    <h1>Add a movie to our database!</h1>
    <form>
      Title:
      <input type="text" v-model="newMovieParams.title" />
      <br />
      Year:
      <input type="text" v-model="newMovieParams.year" />
      <br />
      Plot:
      <input type="text" v-model="newMovieParams.plot" />
      <br />
      <small>{{ 500 - newMovieParams.plot.length }} characters remaining</small>
      <br />
      Director:
      <input type="text" v-model="newMovieParams.director" />
      <br />
      <button v-on:click="createMovie()">Create!</button>
    </form>
  </div>
  <!-- <form>
    <ul>
      <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
    </ul>
    <ul>
      Title:
      <input type="text" v-model="newMovieParams.title" />
    </ul>
    <ul>
      Year:
      <input type="text" v-model="newMovieParams.year" />
    </ul>
    <ul>
      Plot:
      <input type="text" v-model="newMovieParams.plot" />
    </ul>
    <ul>
      Director:
      <input type="text" v-model="newMovieParams.director" />
    </ul>
    <ul>
      English (true/false):
      <input type="text" v-model="newMovieParams.english" />
    </ul>
    <button v-on:submit.prevent="createMovie()">Add Movie!</button>
    <input type="submit" value="create" />
  </form> -->
</template>
