<template>
  <div id="app">
    <div class="container text-center">
      <form
        @submit.prevent="fetchMovies()"
        id="search-movies"
        class="form-inline"
      >
        <input
          v-model="query"
          id="keyword"
          type="text"
          class="form-control ml-auto mr-2"
          placeholder="Find movies"
        />
        <input
          type="submit"
          class="btn btn-primary mr-auto ml-2"
          value="Search"
        />
      </form>
      <div v-if="movies || query === ''">
        <ul id="results" class="list-inline">
          <li v-for="(movie, index) in movies" v-bind:key="index">
            <img :src="movie.Poster" alt="" />
            <p>{{ movie.Title }}</p>
          </li>
        </ul>
      </div>
      <div v-else>
        <p>
          No movies for <strong>{{ query }}</strong>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      movies: [],
      query: "Harry potter",
    };
  },
  methods: {
    fetchMovies() {
      fetch(`http://www.omdbapi.com/?s=${this.query}&apikey=adf1f2d7`)
        .then((res) => res.json())
        .then((data) => (this.movies = data.Search));
    },
  },
  mounted() {
    console.log("Hello");
    this.fetchMovies();
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.blue {
  color: blue;
}
</style>
