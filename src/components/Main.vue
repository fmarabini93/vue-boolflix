<template>
    <main class="text-center">
        <h1 class="text-uppercase mt-5 fw-bold" v-if="filmList.length > 0">Films</h1>
        <div class="d-flex justify-content-around flex-wrap" v-if="filmList.length > 0">
            <div v-for="film in filmList" :key=film-film.id :style='{backgroundImage: `url(https://image.tmdb.org/t/p/w342${film.poster_path}`}' class="m-3 card position-relative border-0">
                <h1 v-if="film.poster_path == null" class="position-absolute top-50 start-50 translate-middle">Poster unavaliable</h1>
                <div class="layover position-absolute top-0 start-0 overflow-auto hidden">
                    <ul class="list-unstyled py-3 position-absolute top-0 start-50 translate-middle-x hidden">
                        <li class="fw-bold text-uppercase fs-3">{{film.title}}</li>
                        <li v-if="film.title != film.original_title" class="fst-italic fs-4">{{film.original_title}}</li>
                        <li>
                            <span v-if="flags.includes(film.original_language)"><img class="flag" :src="require(`../images/${film.original_language}.png`)" alt="`flag ${film.original_language}`"></span>
                            <span class="text-uppercase" v-else>{{film.original_language}}</span>
                        </li>
                        <li>{{film.overview}}</li>
                        <li>
                            <span>
                                <ul v-if="film.vote_average != '0'" class="list-unstyled py-3">
                                    <li class="d-inline-block px-1" v-for="star,index in convertVote(film.vote_average)" :key="index"><i class="fas fa-star"></i></li>
                                    <li class="d-inline-block px-1" v-for="star,index in 5 - convertVote(film.vote_average).length" :key="index"><i class="far fa-star"></i></li>
                                </ul>
                            </span>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
        <h1 class="text-uppercase mt-5 fw-bold" v-if="serieList.length > 0">Series</h1>
        <div class="d-flex justify-content-around flex-wrap" v-if="serieList.length > 0">
            <div v-for="serie in serieList" :key=serie-serie.id :style='{backgroundImage: `url(https://image.tmdb.org/t/p/w342${serie.poster_path}`}' class="m-3 card position-relative border-0">
            <h1 v-if="serie.poster_path == null" class="position-absolute top-50 start-50 translate-middle">Poster unavaliable</h1>
                <div class="layover position-absolute top-0 start-0 overflow-auto hidden">
                    <ul class="list-unstyled py-3 position-absolute top-0 start-50 translate-middle-x hidden">
                        <li class="fw-bold text-uppercase fs-3">{{serie.name}}</li>
                        <li v-if="serie.name != serie.original_name" class="fs-4">{{serie.original_name}}</li>
                        <li>
                            <span v-if="flags.includes(serie.original_language)"><img class="flag" :src="require(`../images/${serie.original_language}.png`)" alt="`flag ${serie.original_language}`"></span>
                            <span class="text-uppercase" v-else>{{serie.original_language}}</span>
                        </li>
                        <li>{{serie.overview}}</li>
                        <li>
                            <span>
                                <ul v-if="serie.vote_average != '0'" class="list-unstyled py-3">
                                    <li class="d-inline-block px-1" v-for="star,index in convertVote(serie.vote_average)" :key="index"><i class="fas fa-star"></i></li>
                                    <li class="d-inline-block px-1" v-for="star,index in 5 - convertVote(serie.vote_average).length" :key="index"><i class="far fa-star"></i></li>
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

export default {
    name: "Main",
    data() {
        return {
            flags: ["en", "it"]
        }
    },
    props: {
        filmList: Array,
        serieList: Array
    },
    methods: {
        convertVote (vote) {
            return new Array(Math.round(vote / 2));
        }
    }
}
</script>

<style lang="scss">
@import '~bootstrap/scss/bootstrap.scss';
    main {

        h1 {
            color: $light;
        }

        .card {
            width: 342px;
            height: 513px;
            box-shadow: 1px 1px 3px 1px $red;
            color: #ffffff;
            background: transparent;

            h1 {
                color: $light;
            }

            .hidden {
                opacity: 0;
            }

            .layover {
                width: 100%;
                height: 100%;
                background-color: rgba($dark,0.8);
            }

            li {
                display: block;
                padding: 10px 0;
                color: $light;
            }

            .flag {
                width: 50px;
            }
        }
        .card:hover {
            .hidden {
                cursor: pointer;
                opacity: 1;
                transition: 0.5s;
            }
        }
    }
</style>