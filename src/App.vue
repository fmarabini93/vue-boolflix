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
        this.getCast(this.films);
      })
      axios.get("https://api.themoviedb.org/3/search/tv?api_key=3631644459350f4e726e4df8e272a6b8&", {
        params: {
          query: text
        }
      })
      .then ((response) => {
        this.series = response.data.results;
        this.text = "";
        this.getCast(this.series);
      })
    },
    getCast(array) {
      array.forEach(
        (element,index) => {
          if (element.original_title) {
            axios.get(`https://api.themoviedb.org/3/movie/${element.id}/credits?api_key=3631644459350f4e726e4df8e272a6b8`)
            .then ((response) => {
              this.films[index].cast = (response.data.cast.slice(0, 5));
            })
          } else {
            axios.get(`https://api.themoviedb.org/3/tv/${element.id}/credits?api_key=3631644459350f4e726e4df8e272a6b8`)
            .then ((response) => {
              this.series[index].cast = (response.data.cast.slice(0, 5));
            }
            )}
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
