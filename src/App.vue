<template>
  <div id="app">
    <Loader />
    <PosterBg :poster="posterBg" />
    <MoviesList :list="moviesList" @changePoster="onChangePoster" />
    <MoviesPagination
      :current-page="currentPage"
      :per-page="moviesPerPage"
      :total="moviesLength"
      @pageChanged="onPageChanged"
    />
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
import MoviesList from "@/components/MoviesList";
import PosterBg from "@/components/PosterBg";
import Loader from "@/components/Loader";
import MoviesPagination from "@/components/MoviesPagination";

export default {
  name: "App",

  data: () => ({
    posterBg: "",
  }),

  components: {
    MoviesList,
    PosterBg,
    MoviesPagination,
    Loader,
  },

  computed: {
    ...mapGetters("movies", [
      "moviesList",
      "moviesPerPage",
      "currentPage",
      "moviesLength",
    ]),
  },

  watch: {
    "$route.query": {
      handler: "onPageQueryChange",
      immediate: true,
      deep: true,
    },
  },

  methods: {
    ...mapActions("movies", ["changeCurrentPage"]),

    onPageQueryChange({ page = 1 }) {
      this.changeCurrentPage(Number(page));
    },

    onChangePoster(poster) {
      this.posterBg = poster;
    },

    onPageChanged(page) {
      // route - состояние текущего маршрута
      // console.log(this.$route);
      // router - набор методов для навигации
      this.$router.push({ query: { page } });
      // this.changeCurrentPage(page);
    },
  },

  created() {
    // if (this.$route.query.page) {
    //   this.changeCurrentPage(Number(this.$route.query.page));
    // }
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
