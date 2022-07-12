<template>
<section>
     <div class="container">
        <div class="card" v-for="film, index in ArrayWatch " :key=index>
            <div class="card-img">
                <img :src="'https:image.tmdb.org/t/p/w342' + film.poster_path" :alt="film.title">
            </div>
        
            <div class="card-info">
                 <h3>{{film.title}}</h3>
                <div>{{film.original_title}}</div>
                <div>{{film.original_lenguage}}</div>
                <div>{{film.vote_average}}</div>
            </div>
           
        </div>
    </div>
</section>
 
</template>

<script>
export default {
    name:'MainComponent',
    props:{
        ArrayWatch: Array
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

            img{
                width: 100%;
                aspect-ratio: 2/3;
                object-fit: cover;
            }
        }

    }
    
    }

</style>