<template>
  <main>
      <div id="search-bar" class="d-flex p-3">
          <input type="text" placeholder="Type to search your film" v-model="searchText">
          <button @click="generateResults">Search</button>
      </div>
      <div id="search-result" class="d-flex justify-content-around flex-wrap">
          <div v-for="film in films" :key=film.id>
              <ul>
                  <li>{{film.title}}</li>
                  <li>{{film.original_title}}</li>
                  <li>{{film.original_language}}</li>
                  <li>{{film.vote_average}}</li>
              </ul>
          </div>
      </div>
  </main>
</template>

<script>
import axios from 'axios';
export default {
    name: "Main",
    data() {
        return {
            films: [],
            searchText: ""
        }
    },
    methods: {
        generateResults() {
            axios.get("https://api.themoviedb.org/3/search/movie?api_key=3631644459350f4e726e4df8e272a6b8&", {
                params: {
                    query: this.searchText
                }
            })
            .then ((response) => {
                this.films = response.data.results;
            })
        }
    }
}
</script>

<style lang="scss">
    #search-bar {
        height: 70px;

        input {
            flex-grow: 1;
        }
    }
    #search-results {
        height: calc(100vh - 70px);
    }
</style>