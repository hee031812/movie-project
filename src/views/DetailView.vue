<template>
    <header id="header" role="banner">
        <div class="header__inner">
            <div class="header__nav">
                <h1>Movie Cinema <span>@</span></h1>
                <nav>
                    <ul>
                        <li><a href="#">Recommend</a></li>
                        <li><a href="#">Top10</a></li>
                    </ul>
                </nav>
            </div>
        </div>
    </header>
    <main class="main">
        <div class="header__intro"
            style="backgroundImage:url(https://image.tmdb.org/t/p/w500/kjQBrc00fB2RjHZB3PGR4w9ibpz.jpg)">
            <div class="container">
                <div class="left play__icon">
                    <a href="#">
                        <img :src="'https://image.tmdb.org/t/p/w500' + movieInfo.poster_path" :alt="movieInfo.title" />
                    </a>
                </div>
                <div class="right">
                    <h2>{{ movieInfo.title }}</h2>
                    <p class="desc">
                        {{ movieInfo.overview }}
                    </p>
                    <p class="date">{{ movieInfo.release_date }}</p>
                    <p class="average">⭐{{ movieInfo.vote_average }}</p>
                    <p class="keyword"></p>
                    <div class="credits">
                        <div class="credits">
                            <div v-for="(credit, index) in credits.cast" :key="credit.id">
                                <img v-if="index < 5 && credit.profile_path"
                                    :src="'https://image.tmdb.org/t/p/w500' + credit.profile_path" :alt="credit.name" />
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </main>
</template>

<script>
import { onMounted, ref } from 'vue';
import { useRoute } from 'vue-router';

export default {
    setup() {
        const movieInfo = ref({});
        const credits = ref([]);
        const route = useRoute();
        const apiKey = 'YOUR_TMDB_API_KEY';

        const movieInfoFetch = async () => {
            const movieId = route.params.movieId;
            try {
                // 영화 정보 가져오기
                const response = await fetch(
                    `https://api.themoviedb.org/3/movie/${movieId}?api_key=9637a8bb3452c234f87e7c25715b7a83&language=ko-KR`
                );
                const data = await response.json();
                movieInfo.value = data;

                // 크레딧 정보 가져오기
                const creditsResponse = await fetch(
                    `https://api.themoviedb.org/3/movie/${movieId}/credits?api_key=9637a8bb3452c234f87e7c25715b7a83&language=ko-KR`
                );
                const creditsData = await creditsResponse.json();
                credits.value = creditsData; // 크레딧 정보 저장

                console.log(data);
                console.log(creditsData);
            } catch (error) {
                console.error('Error fetching movie info:', error);
            }
        };

        const getPersonCredits = async (personId) => {
            try {
                const personCreditsResponse = await fetch(
                    `https://api.themoviedb.org/3/person/${personId}/movie_credits?api_key=9637a8bb3452c234f87e7c25715b7a83&language=ko-KR`
                );
                const personCreditsData = await personCreditsResponse.json();
                console.log(`Person ${personId} credits:`, personCreditsData);

            } catch (error) {
                console.error('Error fetching person credits:', error);
            }
        };

        onMounted(async () => {
            await movieInfoFetch();
            // 크레딧 정보를 받아온 후 각 크레딧의 등장인물 정보를 가져오기 위해 함수 호출
            if (credits.value.cast) {
                for (const credit of credits.value.cast) {
                    await getPersonCredits(credit.id);
                }
            }
        });

        return {
            movieInfo,
            credits,
            getPersonCredits, // 추가: 등장인물의 영화 목록을 가져오는 함수
        };
    },
};
</script>

<style lang="scss">
.header__inner {
    .header__nav {
        display: flex;
        justify-content: space-between;
        align-items: center;

        h1 {
            font-size: 25px;
            font-family: 'LotteriaDdag';
            padding: 3px 1rem;
            margin: 20px 10px;
            display: inline-block;
            text-transform: uppercase;
            color: #ffffff;
            font-weight: 900;
            border: 1px solid #fff;
            position: relative;

            span {
                font-size: 12px;
                align-content: center;
                justify-content: center;
                position: absolute;
                right: 5px;
                top: 0;
                color: #be0000;

            }
        }

        nav {
            li {
                display: inline;

                a {
                    font-weight: 700;
                    display: inline-block;
                    padding: 20px;
                }

                a:hover {
                    color: #ff0000;
                    text-decoration: underline;
                }
            }
        }
    }

}

.header__intro {
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
    position: relative;
    padding: 30px;

    &::before {
        content: '';
        width: 100%;
        height: 100%;
        position: absolute;
        left: 0;
        top: 0;
        background-color: #00000032;
        backdrop-filter: blur(5px);
        z-index: 1;
    }

    .container {
        display: flex;
        justify-content: space-between;
        position: relative;
        z-index: 10;

        .left {
            width: 350px;
        }

        .right {
            width: calc(100% - 390px);

            h2 {
                font-size: 30px;
                margin-bottom: 10px;
            }

            .desc {
                margin-bottom: 10px;
            }

            .credits {
                margin-top: 40px;
                width: 800px;
                display: flex;
                flex-direction: row;

                img {
                    padding: 10px;
                }
            }
        }
    }

}
</style>

