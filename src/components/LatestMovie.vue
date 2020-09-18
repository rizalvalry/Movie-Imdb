<template>
  <v-container v-if="loading">
    <div class="text-xs-center">
      <v-progress-circular indeterminate :size="150" :width="8" color="green"></v-progress-circular>
    </div>
  </v-container>

  <v-container v-else grid-list-xl>
    Sort By :
    <v-card>
      <v-tabs>
        <v-tab
          background-color="deep-purple accent-4"
          center-active
          dark
          v-for="item in items"
          :key="item"
          @click="sort(item)"
        >{{item}}</v-tab>
      </v-tabs>
    </v-card>

    <v-layout wrap>
      <v-flex xs4 v-for="(item, index) in sortMovie" :key="index" mb-2>
        <v-card>
          <v-img :src="item.Poster" aspect-ratio="1"></v-img>
          <v-card-title primary-title>
            <div>
              <h2>{{item.Title}}</h2>
              <div>Year: {{item.Year}}</div>
              <div>Type: {{item.Type}}</div>
              <div>IMDB-id: {{item.imdbID}}</div>
            </div>
          </v-card-title>
          <v-card-actions class="justify-center">
            <v-btn
              depressed
              small
              color="warning"
              class="pa-6 text-center grey lighten-1"
              @click="singleMovie(item.imdbID)"
            >View Details</v-btn>
          </v-card-actions>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import movieApi from "@/services/MovieApi";

export default {
  data() {
    return {
      wholeResponse: [],
      loading: true,
      sorted: false,
      currentSort: "name",
      currentSortDir: "asc",
      select: [],
      items: ["Title", "Year", "Type"],
    };
  },
  mounted() {
    movieApi
      .fetchMovieCollection("power")
      .then((response) => {
        this.wholeResponse = response.Search;
        this.loading = false;
      })
      .catch((error) => {
        console.log(error);
      });
  },
  methods: {
    singleMovie(id) {
      this.$router.push("/movie/" + id);
    },
    sort: function (s) {
      //if s == current sort, reverse
      if (s === this.currentSort) {
        this.currentSortDir = this.currentSortDir === "asc" ? "desc" : "asc";
      }
      this.currentSort = s;
    },
  },
  computed: {
    sortMovie: function () {
      return this.wholeResponse.sort((a, b) => {
        let modifier = 1;
        if (this.currentSortDir === "desc") modifier = -1;
        if (a[this.currentSort] < b[this.currentSort]) return -1 * modifier;
        if (a[this.currentSort] > b[this.currentSort]) return 1 * modifier;
        return 0;
      });
    },
  },
};
</script>

<style lang="stylus" scoped>
.v-progress-circular {
  margin: 1rem;
}
</style>
