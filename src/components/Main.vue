<template>
    <main v-if="filmList.length > 0 || serieList.length > 0" class="text-center">
        <section v-if="filmList.length > 0" class="d-flex justify-content-around flex-wrap">
            <h1 class="text-uppercase">Films</h1>
            <Card v-for="film,index in filmList" :key="'film$-'+film.id+index" :item="film"/>
        </section>
        <section v-if="serieList.length > 0" class="d-flex justify-content-around flex-wrap">
            <h1 class="text-uppercase">Series</h1>
            <Card v-for="serie,index in serieList" :key="serie.id+'-@serie'+index" :item="serie"/>
        </section>
    </main>
    <h1 v-else>Your search didn't match anything</h1>
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