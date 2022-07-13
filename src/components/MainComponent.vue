<template>
<section class="container">
    <h2>FILMS</h2>
    <div class="categories">
        <!-- CARD FILM -->
        <div class="card" v-for="film, index in ArrayFilm " :key= "'f' + index" >
            <img v-if=" film.poster_path !== null " :src="'https:image.tmdb.org/t/p/w342' + film.poster_path" :alt="film.title">
            <img v-else src='http://placehold.jp/70/050505/ff0000/300x500.png?text=POSTER%20NOT%0AFOUND' :alt="film.title">
            <div class="card-info">
                <h3>{{film.title}}</h3>
                <div>{{film.original_title}}</div>
                <img :src="'https://countryflagsapi.com/svg/' + GetRightFlag(film.original_language)" :alt="film.original_language">
                <div><i class="fa-solid fa-star" v-for=" n in 5  " :key="n" :class=" {'star-yellow':n <= VoteWithStar(film.vote_average)}  "></i></div>
                <div class="overview">Trama: {{film.overview}}</div>
            </div>
        </div>
    </div>
    <h2>SERIES</h2>
    <div class="categories">
                <!-- CARD SERIES -->
        <div  class="card" v-for="series, index in ArraySeries " :key= "'s' + index">
            <img v-if=" series.poster_path !== null " :src="'https:image.tmdb.org/t/p/w342' + series.poster_path" :alt="series.name">
            <img v-else src='http://placehold.jp/70/050505/ff0000/300x500.png?text=POSTER%20NOT%0AFOUND' :alt="series.name">
            <div class="card-info">
                <h3>{{series.name}}</h3>
                <div>{{series.original_name}}</div>
                <img :src="'https://countryflagsapi.com/svg/' + GetRightFlag(series.original_language)" :alt="series.original_language">
                <div><i class="fa-solid fa-star" v-for=" n in 5  " :key="n" :class=" {'star-yellow':n <= VoteWithStar(series.vote_average)}  "></i></div>
                <div class="overview">Trama: {{series.overview}}</div>
            </div>
        </div>
    </div>
</section>
 
</template>

<script>

export default {
    name:'MainComponent',
    props:{
        ArrayFilm: Array,
        ArraySeries: Array
    },
    methods:{
        // funzione per modificare alcune iniziali della lingua 
        // per far si che che vengano visualizzate a schermo le bandiere
      GetRightFlag(RightFlag) {

        if(RightFlag == 'en'){
            return RightFlag = "gb";

        } else if(RightFlag == 'ja'){

            return RightFlag = "jp";
        } else if(RightFlag == 'hi'){

            return RightFlag = "in";
        } else if(RightFlag == 'cs'){

            return RightFlag = "cz";
        } else if(RightFlag == 'ko'){

            return RightFlag = "kr";
        }else if(RightFlag == 'sv'){

            return RightFlag = "sc";
        }
        return RightFlag
     },
        // dato il voto lo divido per 2 in modo tale da poter far comparire al massimo 5 stelline
        VoteWithStar(star){
            const StarVote = star/2
            return Math.round(StarVote)   
        },
    }
}
</script>

<style lang="scss" scoped>
    
    .container{
    width: 90%;
    height: 100%;
    margin: 0 auto;

        h2{
            font-size: 25px;
            height: 40px;
            line-height: 40px;
            color: black;
            
        }

        .categories{
            width: 100%;
            display: flex;
            height:calc(50% - 40px);
            overflow-x:auto;
        

            .card{
                width: calc((100% / 7) - 10px);
                margin-right: 10px;
                margin-bottom: 5px;
                flex-shrink: 0;
                aspect-ratio: 2/3;
                position: relative;

                &:hover .card-info{
                    opacity: 0.9;
                }

                img{
                    height: 100%;
                    width: 100%;
                    object-fit: cover;
                }
                
                .card-info{
                    position: absolute;
                    top: 0;
                    bottom: 0;
                    right: 0;
                    left: 0;
                    opacity: 0;
                    background-color: black;
                    color: white;
                    padding: 30px;
                    overflow-y: auto;

                    div{
                        padding-block: 7px;
                    }

                    img{
                        width: 30px;
                        height: auto;
                    }

                    .star-yellow{
                        color: yellow;
                    }
                }
            }
        }
    }
</style>