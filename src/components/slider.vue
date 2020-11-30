<template>
  <section v-if="dataMovies.length > 0" class="d-flex justify-content-center row">
    <div id="movieSlides" class="carousel slide col-12 col-md-3 px-0" data-ride="carousel">
      <ol class="carousel-indicators">
        <li data-target="#movieSlides" :data-slide-to="index" :class="{active: index == 0}" v-for="(movie, index) in dataMovies" :key="index"></li>
      </ol>
      <div class="carousel-inner">
        <div class="carousel-item" :class="{active: index == 0}" v-for="(movie, index) in dataMovies" :key="index">
          <div class="card">
            <div class="card-header p-0 w-100">
              <img class="img-fluid" :src="movie.Poster" :alt="index + 'slide'">
            </div>
            <div class="card-body">
              <p><span class="font-weight-bold">Title: </span><span>{{ movie.Title }}</span></p>
              <p><span class="font-weight-bold">Plot: </span><span>{{movie.Plot}}</span></p>
              <p><span class="font-weight-bold">Plot: </span><span>{{movie.Awards}}</span></p>
            </div>
          </div>
        </div>
      </div>
      <a class="carousel-control-prev d-none d-md-flex" href="#movieSlides" role="button" data-slide="prev">
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="sr-only">Previous</span>
      </a>
      <a class="carousel-control-next d-none d-md-flex" href="#movieSlides" role="button" data-slide="next">
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="sr-only">Next</span>
      </a>
    </div>
  </section>
</template>

<script>
import 'bootstrap'
import axios from 'axios'
const $ = require('jquery')
window.$ = $
let data = ''

export default {
  data() {
    return {
      dataMovies: [],
    }
  },
  methods: {
    fetch: function(query) {
      data = this
      axios({
        method: 'GET',
        url: `http://www.omdbapi.com/?apikey=435c3351&t=${query}`
      }).then(function (response) {
        data.dataMovies.push(response.data)
      }).catch((err) => {
        console.log(err + ' - error in the request')
      })
      console.log(data)
    },
    fillMovies: function() {
      this.fetch('The Avengers')
      this.fetch('Age of ultron')
      this.fetch('black panther')
      this.fetch('avengers endgame')
      console.log(this.dataMovies)
    }
  },
  mounted() {
    this.fillMovies()
  }
}
</script>

<style lang='scss'>
@import '../css/bootstrap.min.css';
#movieSlides {
  .card-body {
    height: 240px;
  }

  img {
    width: 100%;
    height: 500px;
  }
  
}

// Desktop
@media screen and (min-width: 981px) {
  #movieSlides {
    .carousel-control-next {
      right: -75px;
    }

    .carousel-control-prev {
      left: -75px;
    }
  }
}

// Mobile
@media screen and (max-width: 981px) {
  #movieSlides {
    img {
      height: 510px;
    }
  }
}
</style>