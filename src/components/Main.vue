<template>
  <main>
      <div id="search-bar" class="d-flex p-3">
          <input type="text" placeholder="Type to search your film" v-model="searchText" @keyup.enter="generateResults">
          <button @click="generateResults">Search</button>
      </div>
      <div id="search-result" class="d-flex justify-content-around flex-wrap">
          <div v-for="film in films" :key=film.id class="m-3">
              <ul>
                  <li>{{film.title}}</li>
                  <li>{{film.original_title}}</li>
                  <li>
                      <span v-if="film.original_language == 'it'"><img src="../images/it.png" alt="it"></span>
                      <span v-else-if="film.original_language == 'en'"><img src="../images/en.png" alt="en"></span>
                      <span v-else>{{film.original_language}}</span>
                  </li>
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
                this.searchText = "";
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
    #search-result {
        height: calc(100vh - 70px);

        div {
            width: calc(100% / 5 - 40px);

            img {
                width: 40px;
            }
        }
    }
</style>