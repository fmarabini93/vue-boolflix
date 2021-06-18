<template>
    <main class="text-center">
        <section v-if="filmList.length > 0" class="d-flex justify-content-around flex-wrap">
            <h1 v-show="filteredFilms.length > 0" class="text-uppercase">Films</h1>
            <Card v-for="film in filterFilmsByGenre(currentFilmGenre)" :key="film.id" :item="film"/>
        </section>
        <section v-if="serieList.length > 0" class="d-flex justify-content-around flex-wrap p-5">
            <h1 v-show="filteredSeries.length > 0" class="text-uppercase">Series</h1>
            <Card v-for="serie in filterSeriesByGenre(currentSerieGenre)" :key="serie.id" :item="serie"/>
        </section>
    </main>
</template>

<script>
import Card from './Card';

export default {
    name: "Main",
    components: {
        Card
    },
    data() {
        return {
            filteredFilms: [],
            filteredSeries: []
        }
    },  
    props: {
        filmList: Array,
        serieList: Array,
        currentFilmGenre: String,
        currentSerieGenre: String
    },
    methods: {
        filterFilmsByGenre(string) {
            if (string == "") {
                return this.filteredFilms = this.filmList;
            } else {
                return this.filteredFilms = this.filmList.filter((element) => element.genres.map((item) => item.name).includes(string));
            }
        },
        filterSeriesByGenre(string) {
            if (string == "") {
                return this.filteredSeries = this.serieList;
            } else {
                return this.filteredSeries = this.serieList.filter((element) => element.genres.map((item) => item.name).includes(string));
            }
        }
    }
}
</script>