<template>
    <header class="d-flex justify-content-between align-items-center p-3">
        <img src="../images/logo.png" alt="Logo">
        <div>
            <select class="border border-danger" @change="$emit('passFilmGenre', selectedFilmGenre)" v-model="selectedFilmGenre">
                <option hidden>Filter films by genre</option>
                <option v-for="genre,index in fGenList" :key="index">{{genre.name}}</option>
            </select>
            <select class="border border-danger" @change="$emit('passTVGenre', selectedTVGenre)" v-model="selectedTVGenre">
                <option hidden>Filter series by genre</option>
                <option v-for="genre,index in tvGenList" :key="index">{{genre.name}}</option>
            </select>
        </div>
        <div>
            <input type="text" placeholder="Type to search your film" v-model="searchText" @keyup.enter="$emit('passText', searchText)" class="border border-danger border-end-0 p-3">
            <button @click="$emit('passText', searchText)" class="border border-light border-start-0 p-2">Search</button>
        </div>
    </header>
</template>

<script>
export default {
    name: "Header",
    data() {
        return {
            searchText: "",
            selectedFilmGenre: "",
            selectedTVGenre: ""
        }
    },
    props: {
        fGenList: Array,
        tvGenList: Array
    }
}
</script>

<style lang="scss">
@import '~bootstrap/scss/bootstrap.scss';
    header {

        div {
            opacity: 0.7;
        }
        input {
            height: 50px;
            outline: none;
            color: $light;
            background: transparent;
        }
        
        button {
            height: 50px;
            outline: none;
            cursor: pointer;
            color: $red;
            background: transparent;
        }

        select {
            margin: 0 20px;
            color: $light;
            background-color: transparent;
        }
    }
</style>