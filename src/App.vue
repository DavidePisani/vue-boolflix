<template>
  <div id="app">
    <HeaderComponent @FilmsText="UserFilmText" @SeriesText="UserSeriesText"/>
    <main>
      <MainComponent :ArrayFilm="infoFilms" :ArraySeries="infoSeries" />
    </main>
   
  </div>
  
</template>

<script>
import axios from 'axios'
import HeaderComponent from './components/HeaderComponent.vue'
import MainComponent from './components/MainComponent.vue'

export default {
  name: 'App',
  components: {
    HeaderComponent,
    MainComponent,
  },

  data(){
        return{
            SearchText:'',
            SearchFinalText:'',
            urlFilms: 'https://api.themoviedb.org/3/search/movie?api_key=9b421e8c12233512d2be3ddc9ba136cd&language=it-IT&query=',
            infoFilms:[],
            SearchUrlFilms:'',
            urlSeries: 'https://api.themoviedb.org/3/search/tv?api_key=9b421e8c12233512d2be3ddc9ba136cd&language=it-IT&query=',
            infoSeries:[],
            SearchUrlSeries:'',
            
        }
    },

    methods:{
      //testo con + al posto dello spazio e chiamata alle API dei films 
      UserFilmText(text){
          this.SearchText = text;
          this.SearchFinalText = this.SearchText.split(' ').join('+');
          this.SearchUrlFilms = this.urlFilms + this.SearchFinalText;

            axios.get(this.SearchUrlFilms).then((result)=> {
              this.infoFilms = result.data.results
              
            })
      },
  //testo con + al posto dello spazio e chiamata alle API delle series 
      UserSeriesText(text){
          this.SearchText = text;
          this.SearchFinalText = this.SearchText.split(' ').join('+');
          this.SearchUrlSeries = this.urlSeries + this.SearchFinalText;

            axios.get(this.SearchUrlSeries).then((result)=> {
              this.infoSeries = result.data.results
              
            })
      },

      

    }
  }
</script>

<style lang="scss">
@import './assets/style/common';
 
</style>
