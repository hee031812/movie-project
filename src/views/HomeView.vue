<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';


const movies = ref([]);
const searchKeyword = ref('');

const fetchMovies = async (category) => {
  let url = 'https://api.themoviedb.org/3/movie/popular'

  switch (category) {
    case 'latest':
      url = 'https://api.themoviedb.org/3/movie/now_playing'
      break;
    case 'popular':
      url = 'https://api.themoviedb.org/3/movie/popular'
      break;
    case 'upcoming':
      url = 'https://api.themoviedb.org/3/movie/upcoming'
      break;
    case 'toprated':
      url = 'https://api.themoviedb.org/3/movie/top_rated'
      break;
  }

  try {

    const response = await axios.get(url, {
      params: {
        api_key: '9637a8bb3452c234f87e7c25715b7a83',// 실제 API 키로 대체
        language: 'KO-KR',
        page: '1',
      },
    });

    console.log(response); // response.data를 출력하여 실제 데이터를 확인합니다.
    movies.value = response.data.results;
  } catch (err) {
    console.error('Error fetching popular movies:', err);
  }

}
const searchMovies = async () => {
  try {
    const response = await axios.get('https://api.themoviedb.org/3/search/movie', {
      params: {
        api_key: '9637a8bb3452c234f87e7c25715b7a83',// 실제 API 키로 대체
        language: 'KO-KR',
        page: '1',
        query: searchKeyword.value,
      },
    });
    movies.value = response.data.results;
  } catch (err) {
    console.error(err);
  }
}

onMounted(async () => {
  // 초기 페이지 로딩 시 최신 영화를 가져옴
  await fetchMovies('latest');
});



</script>

<template>
  <main>
    <div class="container">
      <div class="movie__inner">
        <h2 class="blind">검색하기</h2>
        <section class="movie__search">
          <input type="search" v-model="searchKeyword" placeholder="검색어를 입력해주세요" @keyup.enter="searchMovies">
          <button type="submit" @click="searchMovies">검색</button>
        </section>
        <div class="movie__tag">
          <ul>
            <li><a href="#" @click="fetchMovies('latest')">최신영화</a></li>
            <li><a href="#" @click="fetchMovies('popular')">인기영화</a></li>
            <li><a href="#" @click="fetchMovies('upcoming')">개봉예정</a></li>
            <li><a href="#" @click="fetchMovies('top_rated')">최고평점</a></li>
          </ul>
        </div>
        <!-- // movie__tag-->


        <section class="movie__cont">
          <h2 class="blind">영화</h2>
          <div class="movie" v-for="movie in movies" :key="movie.id">
            <img :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path" :alt="movie.title">
          </div>
        </section>
        <!-- // movie__cont-->

      </div>
      <!-- //movie__inner -->

    </div>
    <!-- // container-->

  </main>
</template>


<style lang="scss">
.movie__search {
  margin: 50px 0 20px;
  position: relative;

  input {
    border: 1px solid #3d3d3d77;
    padding: 1rem 2rem;
    width: 100%;
    border-radius: 50px;
    background-color: rgba(255, 255, 255, 0.651);
  }

  button {
    position: absolute;
    right: 4px;
    top: 3px;
    width: 45px;
    height: 45px;
    background-color: #3d3d3d77;
    color: #fff;
    border-radius: 50%;
    cursor: pointer;
    font-size: 15px;
  }
}

.movie__tag {
  ul {
    display: flex;

    li {
      a {
        border: 1px solid var(--white);
        padding: 0.5rem 1.3rem;
        display: inline-block;
        border-radius: 20px;
        margin-bottom: 20px;
        margin-right: 10px;
        margin-top: 20px;

        &:hover {
          background-color: var(--white);
          color: var(--black);
        }
      }
    }
  }
}

.movie__cont {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;

  .movie {
    width: 24%;
    margin-bottom: 1.5%;
  }
}
</style>