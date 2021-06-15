<template>
  <main>
      <div id="search-bar" class="d-flex p-3">
          <input type="text" placeholder="Type to search your film" v-model="searchText" @keyup.enter="generateResults">
          <button @click="generateResults">Search</button>
      </div>
      <div id="search-result" class="text-center">
            <h1 class="text-uppercase mt-5" v-if="films.length > 0">Films</h1>
            <div id="filmList" class="d-flex justify-content-around flex-wrap" v-if="films.length > 0">
                <div v-for="film in films" :key=film.id class="m-3 card">
                    <ul class="list-unstyled py-3">
                        <li><img :src="'https://image.tmdb.org/t/p/w342'+film.poster_path" :alt="film.overview"></li>
                        <li>{{film.title}}</li>
                        <li v-if="film.title != film.original_title">{{film.original_title}}</li>
                        <li>
                            <span v-if="film.original_language == 'it'"><img class="flag" src="../images/it.png" alt="it"></span>
                            <span v-else-if="film.original_language == 'en'"><img class="flag" src="../images/en.png" alt="en"></span>
                            <span v-else class="text-uppercase">{{film.original_language}}</span>
                        </li>
                        <li>
                            <span v-if="film.vote_average != '0'">{{film.vote_average}}</span>
                            <span v-else>0 votes</span>
                            <span>
                                <ul class="list-unstyled py-3">
                                    <li class="d-inline-block px-3" v-for="star,index in convertVote(film.vote_average)" :key="index"><i class="fas fa-star"></i></li>
                                </ul>
                            </span>
                        </li>
                    </ul>
                </div>
            </div>
            <h1 class="text-uppercase mt-5" v-if="series.length > 0">Series</h1>
            <div id="seriesList" class="d-flex justify-content-around flex-wrap" v-if="series.length > 0">
                <div v-for="serie in series" :key=serie.id class="m-3 card">
                    <ul class="list-unstyled py-3">
                        <li><img :src="'https://image.tmdb.org/t/p/w342'+serie.poster_path" :alt="serie.overview"></li>
                        <li>{{serie.name}}</li>
                        <li v-if="serie.name != serie.original_name">{{serie.original_name}}</li>
                        <li>
                            <span v-if="serie.original_language == 'it'"><img class="flag" src="../images/it.png" alt="it"></span>
                            <span v-else-if="serie.original_language == 'en'"><img class="flag" src="../images/en.png" alt="en"></span>
                            <span v-else class="text-uppercase">{{serie.original_language}}</span>
                        </li>
                        <li>
                            <span v-if="serie.vote_average != '0'">{{serie.vote_average}}</span>
                            <span v-else>0 votes</span>
                            <span>
                                <ul class="list-unstyled py-3">
                                    <li class="d-inline-block px-3" v-for="star,index in convertVote(serie.vote_average)" :key="index"><i class="fas fa-star"></i></li>
                                </ul>
                            </span>
                        </li>
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
        },
        convertVote (vote) {
            return new Array(Math.round(vote / 2));
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
            width: calc(100% / 3 - 40px);

            li {
                display: block;
                padding: 5px 0;
            }

            .flag {
                width: 40px;
            }
        }
    }
</style>