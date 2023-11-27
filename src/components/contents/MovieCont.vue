<template>
    <section class="movie__cont">
        <h2 class="blind">영화</h2>
        <div class="movie" v-for="movie in movies" :key="movie.id">
            <img :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path" :alt="movie.title">
        </div>
    </section>
</template>