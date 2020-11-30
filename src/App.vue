<template>
  <div>
    <Header/>
    <Slider/>
    <div class="row mt-4">
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
  components: {
    Header, Slider, Movie
  }
}
</script>

<style lang="scss">
@import 'css/bootstrap.min.css';

</style>
