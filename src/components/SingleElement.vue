<script>
export default {
    data() {
        return {

        };
    },
    props: {
        title: String,
        originalTitle: String,
        originalLanguage: String,
        voteAvarage: Number,
        posterImg: String,
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
    
    <div>
        <div>
            <img class="container-img" :src="'https:image.tmdb.org/t/p/w185' + posterImg" :alt="title">
        </div> 

        <div>
            {{ title }}
        </div>

        <div>
            {{ originalTitle }}
        </div>

        <div>
            <img :src="getFlag(originalLanguage)" :alt="originalLanguage">
        </div>

        <div>
            {{ voteAvarage }}
        </div>
        
    </div>
</template>

<style lang="scss" scoped>
img {
    width: 25px;
}

.container-img {
    width: 150px;
}
</style>
