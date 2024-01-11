### vue 사용하여 movie 만들기   

<img width="1903" alt="movie" src="https://github.com/hee031812/recycle-project/assets/144635622/15412a24-df67-4773-9803-71b38fa3edfb">

# 주요 기능
영화 검색: TMDB API를 사용하여 최신 및 인기 영화 정보를 검색하고 표시합니다. 사용자는 다양한 영화를 검색하고 상세 정보를 볼 수 있습니다.
컴포넌트 기반 구조: Vue.js를 사용한 컴포넌트 기반의 접근 방식으로, 사이트의 각 부분을 독립적이고 재사용 가능한 컴포넌트로 구성합니다.
SPA(Single Page Application): Vue Router를 활용하여 싱글 페이지 애플리케이션의 네비게이션을 구현합니다.
상태 관리: Vuex를 사용하여 애플리케이션의 상태를 중앙화하고 효율적으로 관리합니다.
비동기 처리: HTTP 클라이언트를 사용하여 TMDB API에 요청을 보내고, 비동기적으로 데이터를 처리하여 사용자에게 실시간 정보를 제공합니다.

# 설명
이 프로젝트는 Vue.js를 사용하여 구축된 모던 웹 애플리케이션입니다.    
영화 정보를 검색하고 표시하는 기능, 컴포넌트 기반의 구조, SPA 구현, 상태 관리, 그리고 비동기 데이터 처리 등의 기능을 제공합니다.   
개발 환경은 Vue.js, Scss, TMDB API, 그리고 다양한 빌드 및 개발 도구로 구성되어 있습니다.   



1. 우선 사이트[TMDB](https://www.themoviedb.org/?language=ko-KR)에 들어가서 키값을 받아온다.   

### 설치하기   
`npm create vue@latest`   
```bush   
√ Add TypeScript? ... No / Yes   
√ Add JSX Support? ... No / Yes   
√ Add Vue Router for Single Page Application development? ... No / Yes   
√ Add Pinia for state management? ... No / Yes   
√ Add Vitest for Unit Testing? ... No / Yes   
√ Add an End-to-End Testing Solution? » No   
√ Add ESLint for code quality? ... No / Yes   
√ Add Prettier for code formatting? ... No / Yes   
```   
`npm install`   
`npm run format`   
`npm run dev`   

### API 가져오기
TMDB 에서 받아온 키 값을 아래처럼 받아와 작성해준다.

```js
const movies = ref([]);

onMounted(async () => {
  try {
    const response = await axios.get('https://api.themoviedb.org/3/movie/popular?language=en-US&page=1', {
      params: {
        api_key: '9637a8bb3452c234f87e7c25715b7a83'// 실제 API 키로 대체
      },
    });

    console.log(response); // response.data를 출력하여 실제 데이터를 확인합니다.
    movies.value = response.data.results;
    console.log(movies)
  } catch (err) {
    console.error('Error fetching popular movies:', err);
  }
});
```

### 검색한 데이터값 API에 전달하기.
```JS
const searchKeyword = ref(''); // 변수 추가 해주기.


const searchMovies = async () => {
  try {
    const response = await axios.get('https://api.themoviedb.org/3/search/movie', {
      params: {
        api_key: '9637a8bb3452c234f87e7c25715b7a83',// 실제 API 키로 대체
        language: 'KO-KR',
        page: '1',
        query: searchKeyword.value, // API에 전달하기.
      },
    });
    movies.value = response.data.results;
  } catch (err) {
    console.error(err);
  }
}

// input에 v-model 추가
<input type="search" v-model="searchKeyword" placeholder="검색어를 입력해주세요" @keyup.enter="searchMovies">
<button type="submit" @click="searchMovies">검색</button>
```


### 포스트맨 사용법
사이트에서 가져온 주소를 작성한다.
api-key를 주소 방식대로 입력해서 아래 정보를 가져오는지 확인한다.

### Detail view 작업
`movieInfoFetch` 영화 정보를 가져오는 비동기 함수를 사용하였다. 
`credits`에 크레딧 정보를 저장한 후에 등장인물 목록을 가져오는 `getPersonCredits` 함수를 사용하였다.
