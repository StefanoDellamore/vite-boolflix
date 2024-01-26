<script>
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
import AppFooter from './components/AppFooter.vue';
import axios from 'axios';
import { store } from './store.js'

export default {
    data() {
        return {
            store,
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
            .get('https://api.themoviedb.org/3/search/movie?api_key=e35ace60eab40e2d1d8f07320dbae8e6&query=' + this.store.searchText)
            .then((response) => {
                this.store.movies = response.data.results;
            });

            axios
            .get('https://api.themoviedb.org/3/search/tv?api_key=e35ace60eab40e2d1d8f07320dbae8e6&query=' + this.store.searchText)
            .then((response) => {
                this.store.series = response.data.results;
            });
        }
    }
}
</script>

<template>

    <AppHeader @searchExecution="search()" />

    <AppMain />

</template>

<style lang="scss">
@use "assets/scss/main" as *;
@import "assets/scss/partials/reset";
</style>
