<template>
  <div id="app">
    <PosterBg :poster="posterBg" />
    <MoviesList :list="moviesList" @changePoster="onChangePoster" />
    <MoviesPagination/>
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
import MoviesList from "@/components/MoviesList";
import PosterBg from "@/components/PosterBg";
import MoviesPagination from "@/components/MoviesPagination";

export default {
  name: "App",

  data: () => ({
    posterBg: "",
  }),

  components: {
    MoviesList,
    PosterBg,
    MoviesPagination
  },

  computed: {
    ...mapGetters("movies", ["moviesList"]),
  },

  methods: {
    ...mapActions("movies", ["fetchMovies"]),

    onChangePoster(poster) {
      this.posterBg = poster;
    },
  },
};
</script>

<style>
#app {
  font-family: Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  position: relative;
}
</style>
