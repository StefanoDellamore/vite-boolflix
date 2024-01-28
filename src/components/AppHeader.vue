<script>
import { store } from '../store.js';

export default {
    data() {
        return {
            store
        };
    },
}
</script>

<template>
    <header class="background-color">
        <div class="container d-flex justify-content-between p-3 align-items-center">
            <div class="logo-boolflix">
                <img src="/img/boolflix.png" alt="Boolflix">
            </div>
            <div class="input">
                <input v-model="store.searchText" type="text" placeholder="inserisci nome film">

                <button class="style-button" @click="$emit('searchExecution')">
                    search
                </button>
            </div>
        </div>
        
    </header>
</template>

<style lang="scss" scoped>
</style>
