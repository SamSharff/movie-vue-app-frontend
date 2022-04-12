<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Movies! Movies! Movies!",
      movies: [],
      newMovieParams: {},
      currentMovie: {},
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
    createMovie: function () {
      console.log("Creating your movie!");

      axios.post("http://localhost:3000/movies.json", this.newMovieParams).then((response) => {
        console.log("Sucess!", response.data);
        this.movies.push(response.data);
      });
    },
    showMovie: function (movie) {
      console.log(movie);
      this.currentMovie = movie;
      document.querySelector("#movie-details").showModal();
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>New movie!</h2>
    <div>
      Title:
      <input type="text" v-model="newMovieParams.title" />
      <br />
      Year:
      <input type="text" v-model="newMovieParams.year" />
      <br />
      Plot:
      <input type="text" v-model="newMovieParams.plot" />
      <br />
      Director:
      <input type="text" v-model="newMovieParams.director" />
      <br />
      <!-- English (True/False):
      <input type="text" v-model="newMovieParams.english" /> -->
    </div>

    <br />

    <button v-on:click="createMovie">Add a movie</button>
    <div>
      <div v-for="movie in movies" v-bind:key="movie.id">
        <h2>Title: {{ movie.title }}</h2>
        <p>Year: {{ movie.year }}</p>
        <p>Plot: {{ movie.plot }}</p>
        <button v-on:click="showMovie(movie)">More info</button>
      </div>

      <dialog id="movie-details">
        <form method="dialog">
          <h1>Movie info</h1>
          <p>
            Title:
            <input type="text" v-model="currentMovie.title" />
          </p>
          <p>
            Year:
            <input type="text" v-model="currentMovie.year" />
          </p>
          <p>
            Plot:
            <input type="text" v-model="currentMovie.plot" />
          </p>
          <p>
            Director:
            <input type="text" v-model="currentMovie.director" />
          </p>
          <!-- <p>
            English:
            <input type="text" v-model="currentMovie.english" /> -->
          <!-- </p> -->
        </form>
      </dialog>
    </div>
  </div>
</template>

<style></style>
