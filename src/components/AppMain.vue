<script>
import { store } from '../store.js';

export default {
    data() {
        return {
            store
        };
    },
    methods: {

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
                 <div>Original language: {{ movie.original_language }}</div>
                 <div>vote avarage: {{ movie.vote_average }}</div>                                                                                                                       
              </li>
          </ul>
      </div>
  </main>
</template>

<style lang="scss" scoped>
</style>
