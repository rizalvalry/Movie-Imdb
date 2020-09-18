<template>
  <v-app>
    <v-toolbar variant="faded" class="bg-danger" app>
      <a v-bind:href="['/']">
      <img src="./assets/images/imdb-logo.png" class="movie-logo" />
      </a>
      <v-toolbar-title class="headline text-uppercase">
        <router-link to="/" tag="span" style="cursor: pointer"></router-link>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-flex xs12 sm6 md3>
        <v-text-field label="Search Movie.." v-model="searchString"></v-text-field>
      </v-flex>
      <v-btn small color="warning" :disabled="!dataAvailable" @click="searchMovie" dark>
        <span class="mr-2">Search</span>
      </v-btn>
    </v-toolbar>
    <v-content>
      <router-view></router-view>
    </v-content>
    <FooterPanel />
  </v-app>
</template>

<script>
import FooterPanel from '@/components/FooterPanel'

export default {
  name: 'App',
  components: {
    FooterPanel
  },
  data () {
    return {
      searchString: ''
    }
  },
  methods: {
    searchMovie () {
      this.$router.push('/search/' + this.searchString)
      this.searchString = ''
    }
  },
  computed: {
    dataAvailable () {
      return this.searchString !== null && this.searchString !== ''
    }
  }
}
</script>

<style lang="scss" scoped>
@import "./shared/_colours.scss";

.movie-logo {
  width: 65px;
}

.v-toolbar {
  background-image: $gradient;
}

footer {
  text-align: center;
  padding: 15px;
  background-image: $footer;
  width: 100%;
  height: 100px;
}
</style>
