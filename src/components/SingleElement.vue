<script>
export default {
    data() {
        return {
            isHovered: false,
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
        showInfo(value) {
            this.isHovered = value;
        },

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
        
        },
        getVote () {
            return Math.ceil(this.voteAvarage / 2);
        }
    }
}

</script>

<template>
    
    <div class="cover d-flex flex-wrap justify-content-center pt-5" @mouseover="showInfo(true)" @mouseleave="showInfo(false)">
        <div>
            <img class="container-img" :src="'https:image.tmdb.org/t/p/w185' + posterImg" :alt="title">
        </div> 
        <div class="info-container">
            <div>
                <p><strong>Title:</strong>
                    {{ title }}
                </p>
           
            </div>

            <div>
                <p><strong>Original Title:</strong>
                    {{ originalTitle }}
                </p>                
            </div>

            <div>
                <p>
                    <strong>Lang:</strong>
                    <img :src="getFlag(originalLanguage)" :alt="originalLanguage">
                </p>
            </div>

            <div>
                <strong>Vote:</strong>
                <i v-for="i in getVote()" :key="i" class="fa-solid fa-star"></i>
                <i v-for="j in (5 - getVote())" :key="j" class="fa-regular fa-star"></i>
            </div>
        </div>
        
        
    </div>
</template>

<style lang="scss" scoped>

p {
    font-size: 12px;
}

img {
    width: 25px;
}
.container-img {
    width: 170px;
    height: 250px;
}
* {
    color: white;
}

.cover {
    position: relative
}

.info-container {
    padding: 5px;
    width: 170px;
    height: 250px;
    background-color: rgba(0, 0, 0, 0.5);
    position: absolute;
    display: none;
}

.cover:hover .info-container {
  display: block;
}
</style>
