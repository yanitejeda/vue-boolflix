<template>
  <div id="app">
    <input type="text" v-model="query" placeholder="Cerca.."> <button @click="buttonSerch">Search</button>
    <div class="card-movies">
      <ul>
        <li v-for='movie in movies' :key='movie.id' >
          <h2> {{movie.title}} </h2>
          <h3> {{movie.original_title}} </h3>
          <h4>{{movie.original_language}} </h4>
          <img :src="flag[movie.original_language]" alt="">
          <h5>{{movie.vote_average}}</h5>
        </li>
      </ul>

      <ul>
        <li v-for='serie in series' :key='serie.id' >
          <h2> {{serie.name}} </h2>
          <h3> {{serie.original_name}} </h3>
          <h4>{{serie.original_language}} </h4>
          <img :src="flag[serie.original_language]" alt="">
          <h5>{{serie.vote_average}}</h5>
        </li>
      </ul>
      
      
    </div>
   
    
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  components: {},
  data(){
    return{
      apiKey: "ca7354ccd689f61ad128617804bd67af",
      apiUrl:"https://api.themoviedb.org/3",
      movies:[],
      series:[],

      query:"",
      flag:{
        it:require('./assets/it.png'),
        en:require('./assets/en.png'),
}
    };
  },

  methods:{
    buttonSerch(){

      //chiamata axios per avere la lista di oggetti
      axios.get(this.apiUrl +"/search/movie",{
        params:{
          api_key : this.apiKey,

          //ricerca
          query: this.query,
          //scegliere la lingua da stampare
          language:"it",
        },
      })

      .then((resp)=>{
        this.movies = resp.data.results;

      })

       axios.get(this.apiUrl +"/search/tv",{
        params:{
          api_key : this.apiKey,

          //ricerca
          query: this.query,
          //scegliere la lingua da stampare
          language:"it",
        },
      })

      .then((resp)=>{
        this.series = resp.data.results;

      })




    }
    
  }
}
</script>

<style lang="scss">
</style>
