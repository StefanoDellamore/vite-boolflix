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
    <header>
        <input v-model="store.searchText" type="text" placeholder="inserisci nome film">

        <button @click="$emit('searchExecution')">
            search
        </button>
    </header>
</template>

<style lang="scss" scoped>
</style>
