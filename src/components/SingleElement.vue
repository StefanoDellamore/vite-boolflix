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
    height: 25px;
}
</style>
