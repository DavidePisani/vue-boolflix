<template>
  <div id="app">
    <HeaderComponent/>
  </div>
</template>

<script>
import HeaderComponent from './components/HeaderComponent.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    HeaderComponent
  },

  data(){
        return{
            url: 'https://api.themoviedb.org/3/search/movie?api_key=9b421e8c12233512d2be3ddc9ba136cd&language=it-IT&query='
               
        }
    },

  methods{
    AxiosCall(){
      axios.get(this.url)

    }
  }
}
</script>

<style lang="scss">
@import './assets/style/common';

</style>
