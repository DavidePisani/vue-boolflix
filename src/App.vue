<template>
  <div id="app">
    <HeaderComponent @singleText="UserText"/>
    <main>
      <MainComponent :ArrayWatch="infoVideo"/>
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
            url: 'https://api.themoviedb.org/3/search/movie?api_key=9b421e8c12233512d2be3ddc9ba136cd&language=it-IT&query=',
            infoVideo:[],
            SearchUrl:'',
        }
    },

    methods:{
      UserText(text){
          this.SearchText = text;
          this.SearchFinalText = this.SearchText.split(' ').join('+');
          this.SearchUrl = this.url + this.SearchFinalText;

            axios.get(this.SearchUrl).then((result)=> {
              this.infoVideo = result.data.results
              console.log(this.infoVideo)
      })
      },
  

    }
  }
</script>

<style lang="scss">
@import './assets/style/common';

</style>
