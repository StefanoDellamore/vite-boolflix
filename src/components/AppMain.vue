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
            let linkFlag = '';
            if (lang == 'en') {
                linkFlag = 'https://flagicons.lipis.dev/flags/4x3/gb.svg';
            }
            else if (lang == 'ja') {
                linkFlag = 'https://flagicons.lipis.dev/flags/4x3/jp.svg';
            }
            else {
                linkFlag = 'https://flagicons.lipis.dev/flags/4x3/' + lang + '.svg' ;               
            }
            return linkFlag;
        }
    }
}
</script>

<template>
    <main>      
      <div>
          <ul>
              <li v-for="(movie, i) in store.movies" :key="i">
                 <div>Title: {{ movie.title }}</div>
                 <div>Original Title: {{ movie.original_title }}</div>
                 <div>
                    flag:
                    <img :src="getFlag(movie.original_language)" :alt="movie.original_language">
                 </div>
                 <div>vote avarage: {{ movie.vote_average }}</div>                                                                                                                      
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
