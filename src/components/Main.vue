<template>
  <main>
      <div id="search-bar" class="d-flex p-3">
          <input type="text" placeholder="Type to search your film" v-model="searchText" @keyup.enter="generateResults">
          <button @click="generateResults">Search</button>
      </div>
      <div id="search-result">
            <h1 class="text-uppercase" v-if="films.length > 0">Films</h1>
            <div id="filmList" class="d-flex justify-content-around flex-wrap" v-if="films.length > 0">
                <div v-for="film in films" :key=film.id class="m-3 card">
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
            <h1 class="text-uppercase" v-if="series.length > 0">Series</h1>
            <div id="seriesList" class="d-flex justify-content-around flex-wrap" v-if="series.length > 0">
                <div v-for="serie in series" :key=serie.id class="m-3 card">
                    <ul>
                        <li>{{serie.name}}</li>
                        <li>{{serie.original_name}}</li>
                        <li>
                            <span v-if="serie.original_language == 'it'"><img src="../images/it.png" alt="it"></span>
                            <span v-else-if="serie.original_language == 'en'"><img src="../images/en.png" alt="en"></span>
                            <span v-else>{{serie.original_language}}</span>
                        </li>
                        <li>{{serie.vote_average}}</li>
                    </ul>
                </div>
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
            series: [],
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
            axios.get("https://api.themoviedb.org/3/search/tv?api_key=3631644459350f4e726e4df8e272a6b8&", {
                params: {
                    query: this.searchText
                }
            })
            .then ((response) => {
                this.series = response.data.results;
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

        .card {
            width: calc(100% / 5 - 40px);

            img {
                width: 40px;
            }
        }
    }
</style>