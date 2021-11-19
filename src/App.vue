<template>
  <div id="app">
   <!--  <span>
      <i class="far fa-star"></i>
       stella vuota 
      <i class="fa solid fa-star"></i>
      stella piena 
    </span>
 -->
    <input type="text" v-model="query" placeholder="Cerca.." />
    <button @click="buttonSerch">Search</button>
    <div class="card-movies">
      <ul>
        <li v-for="movie in movies" :key="movie.id">
          <h2>{{ movie.title }}</h2>
          <h3>{{ movie.original_title }}</h3>

          <!-- (let i = 0; i < array.length; i++) -->
          <!--  <i class="far fa-star"></i> -->
          <!-- stella vuota -->
          <div>
            <i v-for="i in Math.floor(movie.vote_average / 2)" :key="i"   class="fa solid fa-star"></i>

            <i v-for="i in (5 - Math.floor(movie.vote_average / 2))" :key="i" class="far fa-star"></i>
         </div>


           <!--   <div>{{imgBox(movie.poster_path)}}</div> -->
          <img :src="imgBox(movie.poster_path)" alt="" />
          <h4>{{ movie.original_language }}</h4>
          <img :src="flag[movie.original_language]" alt="" />

          <h5>{{ movie.vote_average }}</h5>
          <h5>{{ Math.floor(movie.vote_average / 2) }}</h5>
        </li>
      </ul>

      <ul>
        <li v-for="serie in series" :key="serie.id">
          <h2>{{ serie.name }}</h2>
          <h3>{{ serie.original_name }}</h3>
          <!--   <div>{{imgBox(serie.poster_path)}}</div> -->

          <!-- <i class="far fa-star"></i> -->
          <!-- stella vuota -->
          <!-- <i class="fa solid fa-star"></i> -->
          <img :src="imgBox(serie.poster_path)" alt="" />

          <h4>{{ serie.original_language }}</h4>
          <img :src="flag[serie.original_language]" alt="" />


          <h5>{{ serie.vote_average }}</h5>
          <h5>{{ Math.floor(serie.vote_average / 2) }}</h5>



          <div>
            <i v-for="i in Math.floor(serie.vote_average / 2)" :key="i"   class="fa solid fa-star"></i>

            <i v-for="i in (5 - Math.floor(serie.vote_average / 2))" :key="i" class="far fa-star"></i>
          </div>

         <!--  <h5>{{ Math.floor(serie.vote_average / 2) }}</h5> -->
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  components: {},

  data() {
    return {
      Object: [],
      apiKey: "ca7354ccd689f61ad128617804bd67af",
      apiUrl: "https://api.themoviedb.org/3",
      movies: [],
      series: [],

      query: "",
      flag: {
        it: require("./assets/it.png"),
        en: require("./assets/en.png"),
      },

      
    };
    
  },

  methods: {
    imgBox(imgEnd) {
      const imgStart = "https://image.tmdb.org/t/p/";
      const imgSize = "w185";

      return imgStart + imgSize + imgEnd;
    },
    buttonSerch() {
      //chiamata per i film
      //chiamata axios per avere la lista di oggetti
      axios
        .get(this.apiUrl + "/search/movie", {
          params: {
            api_key: this.apiKey,

            //ricerca
            query: this.query,
            //scegliere la lingua da stampare
            language: "it",
          },
        })

        .then((resp) => {
          this.movies = resp.data.results;
        });

      //chimata per le serie
      axios
        .get(this.apiUrl + "/search/tv", {
          params: {
            api_key: this.apiKey,

            //ricerca
            query: this.query,
            //scegliere la lingua da stampare
            language: "it",
          },
        })

        .then((resp) => {
          this.series = resp.data.results;
        });
    },

    starC(){
      return Math.floor(this.movie.vote_average)
    }

    


  },

  
};
</script>

<style lang="scss">
@import "@/styles/app";
</style>


