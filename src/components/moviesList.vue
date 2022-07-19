<template>
  <div id="app">
    <div class="container">
      <h1 class="title">Movies</h1>
      <input class="searchInput" type="text" v-model="search" placeholder="Search">
    <div class="movies" v-if="searchMovies.length">
    <movie-card v-for="(movie,index) in searchMovies" :key="index" :movie="movie"></movie-card>
    </div>
    <div class="loading" v-else-if="loading">
        <img src="../assets/images/loading.gif" alt="">
    </div>
    <div class="error" v-else>
        <p>Ma'lumot topilmadi</p>
    </div>
    </div>
  </div>
</template>

<script>
import movieCard  from "@/components/movieCard.vue"
export default {
    components: {
        movieCard
    },
 data() {
  return {
    movies: [],
    loading: false,
    search: ""
  }
 },
 computed: {
  searchMovies() {
    return this.movies.filter(movie => movie.title.uz.toLowerCase().match(this.search.toLowerCase()))
  }
 },
 methods: {
  async getMovies() {
    try{
      this.loading = true
      let response = await fetch("https://api.mediabay.uz/v2/videos/movies?order=new&page=1&size=50");
      let jsonData = await response.json();
      this.movies = jsonData.data
    }
    finally {
      this.loading = false
    }
  }
 },
 mounted() {
  this.getMovies()
 } 
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.title {
    color: #fff;
}
.movies {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
}
.movie {
    flex-basis: 18%;
    margin: 15px 10px;
    height: 400px;
   
}
.img {
    position: relative;
    height: 85%;
}
.movie img {
    width: 100%;
    height: 100%;
}
a {
    text-decoration: none;
}
.year-limit {
    background: #0773FF;
    color: #fff;
    padding: 10px;
    border-bottom-left-radius: 10px;
    position: absolute;
    right: 0;
    font-weight: 600;
}
.name {
    color: #fff;
    margin-top: 5px;
    font-size: 22px;
    font-weight: 600;
}
.loading, .error {
    display: flex;
    flex-direction: column;
    align-items: center;
    color: #fff;
    font-size: 25px;
    margin-top: 10rem;
}
.searchInput {
    border: 1px solid #444;
    outline: none;
    border-radius: 15px;
    background: inherit;
    padding: 10px 15px;
    width: 500px;
    color: #fff;
    margin: 1rem 0;

}
.searchInput::placeholder {
    text-align: center;
    color: #fff;
}

</style>
