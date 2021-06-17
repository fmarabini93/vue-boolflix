<template>

    <!-- Item poster -->
    <section :style='{backgroundImage: `url(https://image.tmdb.org/t/p/w342${item.poster_path}`}' class="m-3 card position-relative border-0">
        <h1 v-if="item.poster_path == null" class="position-absolute top-50 start-50 translate-middle">Poster unavaliable</h1>
    <!-- /Item poster -->
        <!-- Item details -->
        <div class="layover position-absolute top-0 start-0 overflow-auto hidden">
            <h2>{{item.title ? item.title : item.name}}</h2>
            <h5>{{item.original_title ? item.original_title : item.original_name}}</h5>
            <img v-if="flags.includes(item.original_language)" class="flag" :src="require(`../images/${item.original_language}.png`)" alt="`flag ${item.original_language}`">
            <p v-else class="text-uppercase">{{item.original_language}}</p>
            <p>{{item.overview}}</p>
            <hr v-if="item.cast.length > 0">
            <p v-if="item.cast.length > 0" class="fw-bold">Casting:</p>
            <ul v-if="item.cast.length > 0" class="list-unstyled fst-italic">
                <li v-for="actor in item.cast" :key="actor.id">{{actor.name}}</li>
            </ul>
            <hr v-if="item.vote_average != '0'">

            <!-- Convert vote into stars -->
            <ul v-if="item.vote_average != '0'" class="list-unstyled py-3">
                <li class="d-inline-block px-1" v-for="star,index in convertVote(item.vote_average)" :key="`full ${index}`"><i class="fas fa-star"></i></li>
                <li class="d-inline-block px-1" v-for="star,index in 5 - convertVote(item.vote_average).length" :key="index"><i class="far fa-star"></i></li>
            </ul>
            <!-- /Convert vote into stars -->

            <hr v-if="item.genres.length > 0">

            <p v-if="item.genres.length > 0" class="fw-bold">Associated genres:</p>
            <ul v-if="item.genres.length > 0" id="genreList" class="list-unstyled">
                <li v-for="genre,index in item.genres" :key="index" class="d-inline-block px-1">{{genre.name}}</li>
            </ul>

        </div>
        <!-- /Item details -->

    </section>
</template>

<script>
export default {
    name: "Card",
    data() {
        return {
            flags: ["en", "it"]
        }
    },
    props: {
        item: Object
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

    section {
        color: $light;

        .card {
            width: 342px;
            height: 513px;
            box-shadow: 1px 1px 3px 1px $red;
            color: $light;
            background-color: rgba($dark,0.8);

            .hidden {
                opacity: 0;
            }

            .layover {
                width: 100%;
                height: 100%;
                background-color: rgba($dark,0.8);
            }

            .flag {
                width: 50px;
                margin: 10px 0;
            }

            hr {
                width: 70%;
                height: 2px;
                margin: 10px auto;
            }

            #genreList {
                li:not(:last-child)::after {
                    content: " ,";
                }
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