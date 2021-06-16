<template>
    <main class="text-center">
        <section v-if="filmList.length > 0" class="d-flex justify-content-around flex-wrap">
            <h1 class="text-uppercase">Films</h1>
            <Card v-for="film in filmList" :key="film.id" :item="film" />
        </section>
        <section v-if="serieList.length > 0" class="d-flex justify-content-around flex-wrap">
            <h1 class="text-uppercase">Series</h1>
            <Card v-for="serie in serieList" :key="serie.id" :item="serie" />
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
    props: {
        filmList: Array,
        serieList: Array
    }
}
</script>