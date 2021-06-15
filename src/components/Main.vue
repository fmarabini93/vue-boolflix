<template>
  <main>
      <div id="top-bar" class="d-flex justify-content-between align-items-center p-3">
          <img src="../images/logo.png" alt="Logo">
          <div>
                <input type="text" placeholder="Type to search your film" v-model="searchText" @keyup.enter="generateResults" class="border border-danger border-end-0 p-3">
                <button @click="generateResults" class="border border-danger border-start-0 p-2">Search</button>
          </div>
      </div>
      <div id="search-result" class="text-center">
            <h1 class="text-uppercase mt-5 fw-bold" v-if="films.length > 0">Films</h1>
            <div id="filmList" class="d-flex justify-content-around flex-wrap" v-if="films.length > 0">
                <div v-for="film in films" :key=film.id class="m-3 card position-relative">
                    <img :src="'https://image.tmdb.org/t/p/w342'+film.poster_path" :alt="'Poster unavaliable'">
                    <div class="layover position-absolute top-0 start-0 hidden">
                        <ul class="list-unstyled py-3 position-absolute top-50 start-50 translate-middle hidden">
                            <li class="fw-bold text-uppercase fs-1">{{film.title}}</li>
                            <li v-if="film.title != film.original_title" class="fst-italic fs-3">{{film.original_title}}</li>
                            <li>
                                <span v-if="film.original_language == 'it'"><img class="flag" src="../images/it.png" alt="it"></span>
                                <span v-else-if="film.original_language == 'en'"><img class="flag" src="../images/en.png" alt="en"></span>
                                <span v-else class="text-uppercase">{{film.original_language}}</span>
                            </li>
                            <li>{{film.overview}}</li>
                            <li>
                                <span>
                                    <ul v-if="film.vote_average != '0'" class="list-unstyled py-3">
                                        <li class="d-inline-block px-3" v-for="star,index in convertVote(film.vote_average)" :key="index"><i class="fas fa-star"></i></li>
                                        <li class="d-inline-block px-3" v-for="star,index in 5 - convertVote(film.vote_average).length" :key="index"><i class="far fa-star"></i></li>
                                    </ul>
                                </span>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
            <h1 class="text-uppercase mt-5 fw-bold" v-if="series.length > 0">Series</h1>
            <div id="seriesList" class="d-flex justify-content-around flex-wrap" v-if="series.length > 0">
                <div v-for="serie in series" :key=serie.id class="m-3 card position-relative overflow-auto">
                    <img :src="'https://image.tmdb.org/t/p/w342'+serie.poster_path" :alt="'Poster unavaliable'">
                    <div class="layover position-absolute top-0 start-0 hidden">
                        <ul class="list-unstyled py-3 position-absolute top-50 start-50 translate-middle hidden">
                            <li class="fw-bold text-uppercase fs-1">{{serie.name}}</li>
                            <li v-if="serie.name != serie.original_name">{{serie.original_name}}</li>
                            <li>
                                <span v-if="serie.original_language == 'it'"><img class="flag" src="../images/it.png" alt="it"></span>
                                <span v-else-if="serie.original_language == 'en'"><img class="flag" src="../images/en.png" alt="en"></span>
                                <span v-else class="text-uppercase">{{serie.original_language}}</span>
                            </li>
                            <li>{{serie.overview}}</li>
                            <li>
                                <span>
                                    <ul v-if="serie.vote_average != '0'" class="list-unstyled py-3">
                                        <li class="d-inline-block px-3" v-for="star,index in convertVote(serie.vote_average)" :key="index"><i class="fas fa-star"></i></li>
                                        <li class="d-inline-block px-3" v-for="star,index in 5 - convertVote(serie.vote_average).length" :key="index"><i class="far fa-star"></i></li>
                                    </ul>
                                </span>
                            </li>
                        </ul>
                    </div>
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
    #top-bar {
        input {
            height: 50px;
            outline: none;
            background: transparent;

        ::placeholder {
            color: #dc1a28;
        }
        }
        
        button {
            height: 50px;
            margin-left: 20px;
            outline: none;
            cursor: pointer;
            background: transparent;
        }
    }

    #search-result {
        height: calc(100vh - 70px);

        h1 {
            color: #dc1a28;
        }

        .card {
            width: calc(100% / 3 - 40px);
            border: none;
            color: #ffffff;
            background: transparent;

            .hidden {
                opacity: 0;
            }

            .layover {
                width: 100%;
                height: 100%;
                background-color: rgba(0,0,0,0.7);
            }

            li {
                display: block;
                padding: 10px 0;
                color: #ffffff;
            }

            .flag {
                width: 40px;
            }
        }
        .card:hover {
            .hidden {
                opacity: 1;
                transition: 0.5s;
            }
        }
    }
</style>