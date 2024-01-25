<script>
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
import AppFooter from './components/AppFooter.vue';
import axios from 'axios';

export default {
    data() {
        return {
            searchText: '',
            movies: []
        };
    },
    components: {
        AppHeader,
        AppMain,
        AppFooter
    },  
    methods: {
        search() {
            axios
            .get('https://api.themoviedb.org/3/search/movie?api_key=e35ace60eab40e2d1d8f07320dbae8e6&query=' + this.searchText)
            .then((response) => {
                console.log( '1', response.data);
                this.movies = response.data.results;
            });
        }
    }
}
</script>

<template>
    <header>
        <input v-model="searchText" type="text" placeholder="inserisci nome film">
        <button @click="search()">
            search
        </button>
    </header>

    <main>
      
        <div>
            <ul>
                <li v-for="(movie, i) in movies" :key="i">
                    <ul>
                        <li>Title: {{ movie.title }}</li>
                        <li>Original Title: {{ movie.original_title }}</li>
                        <li>Original language: {{ movie.original_language }}</li>
                        <li>vote avarage: {{ movie.vote_avarage }}</li>
                    </ul>
                    
                </li>
            </ul>
        </div>

    </main>
    <!--
    <AppHeader />

    <AppMain />

    <AppFooter />
    -->
</template>

<style lang="scss">
@use "assets/scss/main" as *;
@import "assets/scss/partials/reset";
</style>
