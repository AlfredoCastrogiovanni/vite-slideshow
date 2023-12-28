<script>
    import axios from 'axios';

    export default {
    name: "SlideShow",
    data() {
        return {
            movies: [],
        }
    },
    methods: {
        getDetails(movie_id) {
            let result = "ciao";

            axios.get(`https://api.themoviedb.org/3/movie/${movie_id}`, {
                params: {
                api_key: "5b642de1640631e7141e3df914a0816c",
                language: 'it-IT'
                }
            })
            .then((response) => {
                console.log(response.data);
                this.movies.push(response.data);
            })
            .catch(function (error) {
                console.log(error);
            });
        }
    },
    created() {
        this.getDetails("695721");
        this.getDetails("891699");
        this.getDetails("1029575");
        console.log(this.movies);
    }
    }
</script>

<template>
    <div id="carousel" class="carousel slide" v-if="this.movies.length > 0">
    <div class="carousel-inner">
        <div class="carousel-item" v-for="(movie, index) in movies" :class=" (index == 0) ? 'active' : ''">
        <img :src="(movie.poster_path != null) ? `http://image.tmdb.org/t/p/w500/${movie.backdrop_path}` : '/placeholder.jpg' " class="d-block w-100" :alt="movie.title + '\'s title'">
        <div class="carousel-caption d-none d-md-block">
            <h5 class="text-white">{{ movie.title }}</h5>
        </div>
        </div>
    </div>
    <button class="carousel-control-prev" type="button" data-bs-target="#carousel" data-bs-slide="prev">
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Previous</span>
    </button>
    <button class="carousel-control-next" type="button" data-bs-target="#carousel" data-bs-slide="next">
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Next</span>
    </button>
    </div>
</template>

<style lang="scss" scoped>
        #carousel img {
            height: 900px;
            object-fit: cover;
            object-position: center;
        }
</style>