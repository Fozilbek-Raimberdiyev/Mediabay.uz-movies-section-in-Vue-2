<template>
  <div class="movie">
        <a :href="`https://www.mediabay.uz/movies/movie/${movie.id}`">
          <div class="img">
            <img :src="`${movie.picture}`" alt="movie picture">
            <span class="year-limit">{{movie.yearLimit}}</span>
          </div>
          <p class="name">{{movie.title.uz}}</p>
        </a>
      </div>
</template>

<script>
export default {
props: ["movie"]
}
</script>

<style>

</style>