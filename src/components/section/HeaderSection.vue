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
            <div class="header__intro"
                style="backgroundImage:url(https://image.tmdb.org/t/p/w500/kjQBrc00fB2RjHZB3PGR4w9ibpz.jpg)">
                <div class="container">
                    <div class="left play__icon">
                        <a href="#">
                            <img src="https://image.tmdb.org/t/p/w500/vFsSluuzqxR46Ils9ib52ItdE9u.jpg" alt="dd">
                        </a>
                    </div>
                    <div class="right">
                        <h2>크리에이터</h2>
                        <p class="desc">
                            인류를 지키기 위해 만들어진 AI가 LA에 핵폭탄을 터뜨린 후, 인류와 AI 간의 피할 수 없는 전쟁이 시작된다. 전직 특수부대 요원 ‘조슈아’는
                            실종된 아내의 단서를 얻을지도 모른다는 생각에 전쟁을 끝내기 위한 인류의 작전에 합류한다. 인류를 위협할 강력한 무기와 이를 창조한 ‘창조자’를 찾아 나서고, 그 무기가
                            아이 모습의 AI 로봇 '알피'란 사실을 알게 되는데… 인간적인가, 인간의 적인가? 10월, SF 블록버스터의 신세계가 펼쳐진다!
                        </p>
                        <p class="date">개봉 : 2023-09-27</p>
                        <p class="average">평점 : 7.1</p>
                        <div class="credits">
                            <div>
                                <img src="https://image.tmdb.org/t/p/w500/yirl6fEmeXY5xcvJw3nTcCNq9Cw.jpg" alt="">
                            </div>
                            <div>
                                <img src="https://image.tmdb.org/t/p/w500/6Yk5t9RwkdkAT8Qv45934Eez2CA.jpg" alt="">
                            </div>
                            <div>
                                <img src="https://image.tmdb.org/t/p/w500/8XJzD4mrxlBvtYjP1wVNTW5K9ya.jpg" alt="">
                            </div>
                            <div>
                                <img src="https://image.tmdb.org/t/p/w500/e9XlcFnZQiBSQ1vISQVyTOrkIaq.jpg" alt="">
                            </div>
                            <div>
                                <img src="https://image.tmdb.org/t/p/w500/6u95ZNLrADSlK7CVkgEvC0jLIJh.jpg" alt="">
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </header>
</template>
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

            span {
                font-size: 12px;
                align-content: center;
                justify-content: center;
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
