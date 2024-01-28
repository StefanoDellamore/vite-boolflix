<script>
import SingleElement from './SingleElement.vue';
import { store } from '../store.js';

export default {
    data() {
        return {
            store
        };
    },
    components: {
        SingleElement
    },
    methods: {
        getFlag (lang) {
            let linkFlag = 'https://flagicons.lipis.dev/flags/4x3/';
            const validLang = [
                'ja',
                'en',
                'fr',
                'pt',
                'de',
                'es',
                'it',       
            ];

            if (validLang.includes(lang)) {
                if (lang == 'en') {
                    linkFlag += 'gb';
                }
                else if (lang == 'ja') {
                    linkFlag += 'jp';
                }
                else {
                    linkFlag += lang;
                }
            }
            else {
                linkFlag += 'un';
            }
            linkFlag += '.svg';

            return linkFlag;
        
        }
    }
}
</script>

<template>
    <main class="background-color">
        <div class="container-title">
            <h2>MOVIES</h2> 
        </div>
        <div class="container">                           
            <div>
                <ul>
                    <li v-for="(movie, i) in store.movies" :key="i">
                        <SingleElement 
                        :title="movie.title"
                        :originalTitle="movie.original_title"
                        :originalLanguage="movie.original_language"
                        :voteAvarage="movie.vote_average"
                        :posterImg="movie.poster_path"
                        />                                                                                                                     
                    </li>
                </ul>
            </div>
        </div>
        
        <br>

        <div class="container-title">
            <h2>SERIES</h2> 
        </div>

        <div class="container">
            <div>
                <ul>
                    <li v-for="(serie, i) in store.series" :key="i">
                        <SingleElement 
                        :title="serie.name"
                        :originalTitle="serie.original_name"
                        :originalLanguage="serie.original_language"
                        :voteAvarage="serie.vote_average"
                        :posterImg="serie.poster_path"
                        />                                                                                                                     
                    </li>
                </ul>
            </div>
        </div>
       
  </main>
</template>

<style lang="scss" scoped>
li {
    list-style: none;
}

.container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}
.container-title {
    width: 100%;
    margin-bottom: 10px;
}
ul {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    padding: 0;
}

li {
    flex: calc(33.33% - 10px);
    margin-bottom: 20px;
}

</style>
