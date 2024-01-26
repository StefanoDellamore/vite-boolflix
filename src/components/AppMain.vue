<script>
import { store } from '../store.js';

export default {
    data() {
        return {
            store
        };
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
    <main>
        <h2>movies</h2>     
        <div>
            <ul>
                <li v-for="(movie, i) in store.movies" :key="i">
                    <div>Title: {{ movie.title }}</div>
                    <div>Original Title: {{ movie.original_title }}</div>
                    <div>                        
                        <img :src="getFlag(movie.original_language)" :alt="movie.original_language">
                    </div>
                    <div>vote avarage: {{ movie.vote_average }}</div>                                                                                                                      
                </li>
            </ul>
        </div>

        <br>

        <h2>series</h2>     
        <div>
            <ul>
                <li v-for="(serie, j) in store.series" :key="j">
                    <div>Title: {{ serie.name }}</div>
                    <div>Original Title: {{ serie.original_name }}</div>
                    <div>
                        <img :src="getFlag(serie.original_language)" :alt="serie.original_language">
                    </div>
                    <div>vote avarage: {{ serie.vote_average }}</div>                                                                                                                      
                </li>
            </ul>
        </div>
        
  </main>
</template>

<style lang="scss" scoped>

img {
    height: 25px;
}
</style>
