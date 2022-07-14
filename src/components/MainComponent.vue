<template>
<section class="container">
    <h2>FILMS</h2>
    <div class="categories">
        <!-- CARD FILM -->
        <div class="card" v-for="element, index in ArrayFilm " :key= "'f' + index" >
            <img v-if=" element.poster_path !== null " :src="'https:image.tmdb.org/t/p/w342' + element.poster_path" :alt="element.title">
            <img v-else src='http://placehold.jp/70/050505/ff0000/300x500.png?text=POSTER%20NOT%0AFOUND' :alt="element.title">
            <div @mouseenter="GetCast(element.id)" class="card-info">
                <h3>{{element.title}}</h3>
                <div>{{element.original_title}}</div>
                <div v-for="name, index in CastArray " :key="index">{{name}}</div>
                <img :src="'https://countryflagsapi.com/svg/' + GetRightFlag(element.original_language)" :alt="element.original_language">
                <div><i class="fa-solid fa-star" v-for=" n in 5  " :key="n" :class=" {'star-yellow':n <= VoteWithStar(element.vote_average)}  "></i></div>
                <div>Trama: {{element.overview}}</div>
            </div>
        </div>
    </div>
    <h2>SERIES</h2>
    <div class="categories">
                <!-- CARD SERIES -->
        <div  class="card" v-for="element, index in ArraySeries " :key= "'s' + index">
            <img v-if=" element.poster_path !== null " :src="'https:image.tmdb.org/t/p/w342' + element.poster_path" :alt="element.name">
            <img v-else src='http://placehold.jp/70/050505/ff0000/300x500.png?text=POSTER%20NOT%0AFOUND' :alt="element.name">
            <div class="card-info">
                <h3>{{element.name}}</h3>
                <div>{{element.original_name}}</div>
                <img :src="'https://countryflagsapi.com/svg/' + GetRightFlag(element.original_language)" :alt="element.original_language">
                <div><i class="fa-solid fa-star" v-for=" n in 5  " :key="n" :class=" {'star-yellow':n <= VoteWithStar(element.vote_average)}  "></i></div>
                <div>Trama: {{element.overview}}</div>
            </div>
        </div>
    </div>
</section>
 
</template>

<script>
    import axios from 'axios'
export default {
    name:'MainComponent',
    props:{
        ArrayFilm: Array,
        ArraySeries: Array
    },

    data(){
        return{
            CastArray:[]
        }
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

        GetCast(identify){
            this.CastArray = [];
            axios.get(`https://api.themoviedb.org/3/movie/${identify}/credits?api_key=9b421e8c12233512d2be3ddc9ba136cd&language=it-It`).then(response => {
                if(response.data.cast.length >= 5){
                     for(let i = 0; i < 5; i++){
                        this.CastArray.push(response.data.cast[i].name);
                    }
                     console.log('ciclo for 1') 
                }else if(response.data.cast.length <= 4){
                    for(let i = 0; i < response.data.cast.length; i++){
                        this.CastArray.push(response.data.cast[i].name);
                    }
                    console.log('ciclo for 2') 
                }else{
                    this.CastArray.push("no cast found");
                }
                    this.CastArray;
            })
        }
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
                width: calc((100% / 6) - 10px);
                margin-right: 10px;
                margin-bottom: 5px;
                flex-shrink: 0;
                aspect-ratio: auto;
                position: relative;

                &:hover .card-info{
                    opacity: 1;
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
                    background-color: rgba($color: #000000, $alpha: 0.8);
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