<template>
  <div class="movies">
    <h1>영화 목록</h1>
    <div v-for="movie in movies" v-bind:key="movie.id" class="movie">
      <img v-bind:src="movie.poster" class="poster">
      <div>
        <strong>{{movie.name}}</strong>, <i>{{movie.director}}</i> [{{movie.year}}]
        <router-link :to="{ name: 'show', params: { id: movie.id }}">더보기</router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  created () {
    this.$http.get('/api/movies')
    .then((response) => {
      this.movies = response.data
    })
  },
  name: 'hello',
  data () {
    return {
      movies: []
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.poster {
  width: 185px;
  vertical-align: middle;
}

.movie {
  display: inline-block;
  padding: 10px;
  text-align: center;
}
</style>
