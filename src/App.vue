<template>
  <div id="app">
    <Header @passText='generateResults'/>
    <Main :filmList='films' :serieList='series'/>
  </div>
</template>

<script>
import axios from 'axios';
import Header from './components/Header'
import Main from './components/Main';

export default {
  name: 'App',
  components: {
    Header,
    Main
  },
  data() {
    return {
      films: [],
      series: []
    }
  },
  methods: {
    generateResults(text) {
            axios.get("https://api.themoviedb.org/3/search/movie?api_key=3631644459350f4e726e4df8e272a6b8&", {
                params: {
                    query: text
                }
            })
            .then ((response) => {
                this.films = response.data.results;
                this.text = "";
            })
            axios.get("https://api.themoviedb.org/3/search/tv?api_key=3631644459350f4e726e4df8e272a6b8&", {
                params: {
                    query: text
                }
            })
            .then ((response) => {
                this.series = response.data.results;
                this.text = "";
            })
    }
  }
}
</script>

<style lang="scss">
@import '~@fortawesome/fontawesome-free/css/all.min.css';
@import '~bootstrap/scss/bootstrap.scss';
$red: #dc1a28;

  body {
    background-color: $dark;
  }
</style>
