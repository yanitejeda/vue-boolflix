<template>
  <div id="app">
    <!--  <span>
      <i class="far fa-star"></i>
       stella vuota 
      <i class="fa solid fa-star"></i>
      stella piena 
    </span>
 -->
    <!-- nav -->
    <div class="box-container">
      <div>
        <h1>BoolFlix</h1>
      </div>
      <div>
        <input type="text" v-model="query" placeholder="Cerca.." />
        <button @click="buttonSerch">Search</button>
      </div>
    </div>

    <div class="card-movies box-container-card">
      <div>
        <h1>movies</h1>
        <ul>
          <li class="card-box" v-for="movie in movies" :key="movie.id">
            <div class="box-img">
              <h3 class="tittle">{{ movie.title }}</h3>
              <!--   <div>{{imgBox(movie.poster_path)}}</div> -->
              <img :src="imgBox(movie.poster_path)" alt="" />

              <div class="hover-p">
                <h3>{{ movie.original_title }}</h3>
                <h5>{{ movie.vote_average }}</h5>

                <div>
                  <i
                    v-for="i in 5 "
                    :key="`m-${movie.id}-${i}`"
                    :class="i <= getStars(movie.vote_average) ? 'fa solid fa-star' : 'far fa-star'"
                  ></i>
                  
                </div>
                <div>
                  <h4>{{ movie.original_language }}</h4>
                  <img
                    class="flag-w"
                    :src="flag[movie.original_language]"
                    alt=""
                  />
                </div>
              </div>
            </div>
          </li>
        </ul>
      </div>

      <div>
        <h1>series</h1>
        <ul>
          <li class="card-box" v-for="serie in series" :key="serie.id">
            <div class="box-img">
              <h3 class="tittle">{{ serie.name }}</h3>
              <img :src="imgBox(serie.poster_path)" alt="" />
              <div class="hover-p">
                <h3>{{ serie.original_name }}</h3>
                <h5>{{ serie.vote_average }}</h5>

                <div>
                  <i
                    v-for="i in 5"
                    :key="`s-${serie.id}-${i}`"
                    :class="i <= getStars(serie.vote_average) ? 'fa solid fa-star' : 'far fa-star'"
                  ></i>
                </div>

                <div>
                  <h4>{{ serie.original_language }}</h4>
                  <img
                    class="flag-w"
                    :src="flag[serie.original_language]"
                    alt=""
                  />
                </div>
              </div>
            </div>
          </li>
        </ul>
      </div>
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
    getStars(vote){
      return  Math.floor(vote / 2)

    },

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

    starC() {
      return Math.floor(this.movie.vote_average);
    },

    
  },
};
</script>

<style lang="scss">
@import "@/styles/app";
@import "@/styles/appStyle";
</style>


