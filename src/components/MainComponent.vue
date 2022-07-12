<template>
<section>
     <div class="container">
        <div class="card" v-for="film, index in ArrayFilm " :key = "f + index">
            <div class="card-img">
                <img :src="'https:image.tmdb.org/t/p/w780' + film.poster_path" :alt="film.title">
            </div>
            <div class="card-info">
                <h3>{{film.title}}</h3>
                <div>{{film.original_title}}</div>
                <img :src="'https://countryflagsapi.com/svg/' + GetRightFlag(film.original_language)" :alt="film.original_language">
                <div>{{film.vote_average}}</div>
            </div>
        </div>

        <div class="card" v-for="series, index in ArraySeries " :key = "s + index">
            <div class="card-img">
                <img :src="'https:image.tmdb.org/t/p/w780' + series.backdrop_path" :alt="series.name">
            </div>
            <div class="card-info">
                <h3>{{series.name}}</h3>
                <div>{{series.original_title}}</div>
                <img :src="'https://countryflagsapi.com/svg/' + GetRightFlag(series.original_language)" :alt="series.original_language">
                <div>{{series.vote_average}}</div>
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

    }
}
</script>

<style lang="scss" scoped>
    section{
        width: 100%;
        
        .container{
        width: 90%;
        margin: 0 auto;
        display: flex;
        flex-wrap: wrap;
        padding: 10px;

        .card{
            width: calc((100% / 5) - 10px);
            margin: 5px;
            background-color: white;
            position: relative;

            &:hover .card-info{
                opacity: 0.9;
            }

            .card-img{
                img{
                    width: 100%;
                    aspect-ratio: 2/3;
                    object-fit: cover;
                }
               
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

                div{
                    padding-block: 10px;
                }

                img{
                    width: 30px;
                }
            }
        }

    }
    
    }

</style>