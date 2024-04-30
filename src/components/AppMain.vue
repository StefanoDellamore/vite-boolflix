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
}

//Movie
document.addEventListener('DOMContentLoaded', () => {
    const apiKey = 'e35ace60eab40e2d1d8f07320dbae8e6';
    const defaultQuery = 'popular';
    
    fetch(`https://api.themoviedb.org/3/search/movie?api_key=${apiKey}&query=${defaultQuery}`)
        .then(response => response.json())
        .then(data => {
            const firstThreeMovies = data.results.slice(0, 3);
            displayMovies(firstThreeMovies);
        })
        .catch(error => {
            console.error('Error fetching data:', error);
        });
});

function displayMovies(movies) {
    const movieResultsDiv = document.getElementById('movieResults');
    movieResultsDiv.innerHTML = '';

    if (movies.length === 0) {
        movieResultsDiv.textContent = 'No movies found.';
        return;
    }

    movies.forEach(movie => {
        const movieItem = createMovieElement(movie);
        movieResultsDiv.appendChild(movieItem);
    });
}

function createMovieElement(movie) {
    const movieItem = document.createElement('div');
    movieItem.classList.add('movie-item');

    if (movie.poster_path) {
        const posterUrl = `https://image.tmdb.org/t/p/w500${movie.poster_path}`;
        const posterImg = document.createElement('img');
        posterImg.src = posterUrl;
        posterImg.alt = movie.title;
        movieItem.appendChild(posterImg);
    }

    const titleElement = document.createElement('h2');
    titleElement.textContent = movie.title;
    movieItem.appendChild(titleElement);

    if (movie.overview) {
        const overviewElement = document.createElement('p');
        overviewElement.textContent = movie.overview;
        movieItem.appendChild(overviewElement);
    }
 
    if (movie.release_date) {
        const releaseDateElement = document.createElement('p');
        releaseDateElement.textContent = `Release Date: ${movie.release_date}`;
        movieItem.appendChild(releaseDateElement);
    }

    if (movie.vote_average) {
        const ratingElement = document.createElement('p');
        ratingElement.textContent = `Rating: ${movie.vote_average}/10`;
        movieItem.appendChild(ratingElement);
    }

    return movieItem;
}

//Serie
document.addEventListener('DOMContentLoaded', () => {
    const apiKey = 'e35ace60eab40e2d1d8f07320dbae8e6';
    const defaultQuery = 'popular';

    fetch(`https://api.themoviedb.org/3/search/tv?api_key=${apiKey}&query=${defaultQuery}`)
        .then(response => response.json())
        .then(data => {
            const firstThreeSeries = data.results.slice(0, 3);
            displaySeries(firstThreeSeries);
        })
        .catch(error => {
            console.error('Error fetching data:', error);
        });
});

function displaySeries(series) {
    const seriesResultsDiv = document.getElementById('serieResults');
    seriesResultsDiv.innerHTML = '';

    if (series.length === 0) {
        seriesResultsDiv.textContent = 'No series found.';
        return;
    }

    series.forEach(serie => {
        const serieItem = createSerieElement(serie);
        seriesResultsDiv.appendChild(serieItem);
    });
}

function createSerieElement(serie) {
    const serieItem = document.createElement('div');
    serieItem.classList.add('serie-item');

    if (serie.poster_path) {
        const posterUrl = `https://image.tmdb.org/t/p/w500${serie.poster_path}`;
        const posterImg = document.createElement('img');
        posterImg.src = posterUrl;
        posterImg.alt = serie.name;
        serieItem.appendChild(posterImg);
    }

    const titleElement = document.createElement('h2');
    titleElement.textContent = serie.name;
    serieItem.appendChild(titleElement);

    if (serie.overview) {
        const overviewElement = document.createElement('p');
        overviewElement.textContent = serie.overview;
        serieItem.appendChild(overviewElement);
    }

    if (serie.first_air_date) {
        const releaseDateElement = document.createElement('p');
        releaseDateElement.textContent = `First Air Date: ${serie.first_air_date}`;
        serieItem.appendChild(releaseDateElement);
    }

    if (serie.vote_average) {
        const ratingElement = document.createElement('p');
        ratingElement.textContent = `Rating: ${serie.vote_average}/10`;
        serieItem.appendChild(ratingElement);
    }

    return serieItem;
}

</script>

<template>
    <main class="background-color">
        <div class="container-title">
            <h2>MOVIES</h2> 
        </div>

        <div id="movieResults" class="movie-grid" ></div>

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

        <div id="serieResults" class="movie-grid" ></div>

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

.movie-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
}

.movie-item {
    border: 1px solid #ccc;
    padding: 10px;
    text-align: center;
}

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
