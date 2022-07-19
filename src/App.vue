<template>
  <MovieList></MovieList>
</template>

<script>
import MovieList from "@/components/moviesList.vue"
export default {
  components : {
    MovieList
  }
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    user-select: none;
} 
body {
    background: #272727;
}
.container {
    width: 1250px;
    margin: 0 auto;
}
</style>