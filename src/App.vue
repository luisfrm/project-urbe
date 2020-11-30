<template>
  <div>
    <Header/>
    <Slider/>
    <div v-if="movies.length > 0" id="movies" class="row mt-4">
      <div class="col-12 col-md-4">
        <Movie/>
      </div>
    </div>
  </div>
</template>

<script>
import Header from './components/header'
import Slider from './components/slider'
import Movie from './components/movie-container'

export default {
  name: 'App',
  data() {
    return {
      movies: []
    }
  },
  components: {
    Header, Slider, Movie
  }
}
</script>

<style lang="scss">
@import 'css/bootstrap.min.css';

</style>
