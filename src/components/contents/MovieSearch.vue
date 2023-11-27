<template>
    <section class="movie__search">
        <input type="search" v-model="searchKeyword" placeholder="검색어를 입력해주세요" @keyup.enter="searchMovies">
        <button type="submit" @click="searchMovies">검색</button>
    </section>
</template>

<script>
export default {

}
</script>