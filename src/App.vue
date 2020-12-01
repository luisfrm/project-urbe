<template>
  <div>
    <Header/>
    <Slider/>
    <div v-if="movies.length > 0" id="movies" class="row mt-4 px-5 my-4 w-100">
      <div v-for="(movie, index) in movies" :key="index" class="col-12 col-md-3 movie-container my-5">
        <Movie
        @click="selectMovie(index)"
        :img="movie.Poster"
        :title="movie.Title"
        :plot="movie.Plot"
        :id="index"
        :rating="movie.imdbRating"
        :runtime="movie.Runtime"
        :genre="movie.Genre"
        data-toggle="modal"
        data-target="#details-modal"
        />
      </div>
    </div>

    <!-- Details modal -->
    <div class="modal fade" id="details-modal" tabindex="-1" role="dialog" aria-labelledby="details-modal-Label" aria-hidden="true">
      <div class="modal-dialog modal-md" role="document">
        <div class="modal-content">
          <div class="modal-header justify-content-center p-0">
            <div class="row w-100">
              <div class="col-12 px-0 py-2">
                <button type="button" class="close mr-0" data-dismiss="modal" aria-label="Close">
                  <span aria-hidden="true">&times;</span>
                </button>
              </div>
              <div class="col-12 px-0 d-flex justify-content-center">
                <img :src="detailsMovie.Poster ? detailsMovie.Poster : 'https://i.imgur.com/EPDBVqq.jpg'" :alt="'image'" class="img-fluid">
              </div>
            </div>
          </div>
          <div class="modal-body">
            <p class="body-title" v-if="detailsMovie.Title">{{detailsMovie.Title}}</p>
            <p class="body-text" v-if="detailsMovie.Plot">{{detailsMovie.Plot}}</p>
            <p class="body-text" v-if="detailsMovie.Runtime"><span class="font-weight-bold">Runtime: </span> {{detailsMovie.Runtime}}</p>
            <p class="body-text" v-if="detailsMovie.Rating"><span class="font-weight-bold">Rating: </span>{{detailsMovie.Rating}}</p>
            <p class="body-text" v-if="detailsMovie.Genre"><span class="font-weight-bold">Genre: </span>{{detailsMovie.Genre}}</p>
            <p class="body-text" v-if="detailsMovie.Actors"><span class="font-weight-bold">Actors: </span>{{detailsMovie.Actors}}</p>
            <p class="body-text" v-if="detailsMovie.Rated"><span class="font-weight-bold">Rated: </span>{{detailsMovie.Rated}}</p>
            <p class="body-text" v-if="detailsMovie.Released"><span class="font-weight-bold">Released: </span>{{detailsMovie.Released}}</p>
            <p class="body-text" v-if="detailsMovie.Awards"><span class="font-weight-bold">Awards: </span>{{detailsMovie.Awards}}</p>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-outline-success" data-dismiss="modal">Close</button>
          </div>
        </div>
      </div>
    </div>

    <!-- Modal de about us -->
    <div class="modal fade" id="aboutme-modal" tabindex="-1" role="dialog" aria-labelledby="details-modal-Label" aria-hidden="true">
      <div class="modal-dialog modal-md" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title body-title">{{ data_about.title && name ? `${data_about.title} · ${name}` : 'About Me' }}</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <p v-if="data_about.WhoAmI">{{data_about.WhoAmI}}</p>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-outline-success" data-dismiss="modal">Close</button>
          </div>
        </div>
      </div>
    </div>

    <!-- Modal de about it -->
    <div class="modal fade" id="aboutit-modal" tabindex="-1" role="dialog" aria-labelledby="details-modal-Label" aria-hidden="true">
      <div class="modal-dialog modal-md" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title body-title">{{ data_aboutit.title && nameApp ? `${data_aboutit.title} · ${nameApp}` : 'WikiMovie' }}</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body p-0">
            <ul class="list-group">
              <li class="list-group-item bg-success">How it was created?</li>
              <li class="list-group-item" v-for="(item, index) in data_aboutit.howItWasCreated" :key="index">
                <p>{{item}}</p>
              </li>
            </ul>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-outline-success" data-dismiss="modal">Close</button>
          </div>
        </div>
      </div>
    </div>

    <!-- Modal de contact us -->
    <div class="modal fade" id="contactme-modal" tabindex="-1" role="dialog" aria-labelledby="details-modal-Label" aria-hidden="true">
      <div class="modal-dialog modal-md" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title body-title">{{ data_contact.title && name ? `${data_contact.title} · ${name}` : 'Contact Me' }}</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body p-0">
            <ul class="list-group">
              <li class="list-group-item bg-success">Emails</li>
              <li class="list-group-item" v-for="(email, index) in data_contact.emails" :key="index">
                {{email}}
              </li>
              <li class="list-group-item bg-success">Phone number</li>
              <li class="list-group-item" v-for="(tlf, index) in data_contact.tlfs" :key="index">
                {{tlf}}
              </li>
            </ul>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-outline-success" data-dismiss="modal">Close</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Header from './components/header'
import Slider from './components/slider'
import Movie from './components/movie-container'

export default {
  name: 'App',
  data() {
    return {
      movies: [],
      detailsMovie: {},
      data_contact: {
        title: 'Contact Me',
        emails: [
          'luisfrm_@outlook.com',
          'luis@321ignition.com'
        ],
        tlfs: [
          '+58412-4722407'
        ]
      },
      data_about: {
        title: "About me",
        WhoAmI: "I'm a young programmer, a student of computing. I Work in 321 Ignition like Programmer Front end since begins of this year. I have done some web apps and desktop apps, I like everything about it, I wish I could graduate soon and keep working on this"
      },
      data_aboutit: {
        title: "About it",
        howItWasCreated: [
          "This app web was created working with multiple technologies current like:",
          "Node Package Manager, also NPM, this technology was used to manage the packages used, like Vue JS, Bootstrap, Axios, Jquery, PooperJS",
          "VueJs, used like Framework in the Front end, using also components created with this technology.",
          `Axios, this library was used to make the requests to the API of <a href="http://www.omdbapi.com/" target="_blank">omdbapi</a>`,
          "Bootstrap, the framework of CSS used for this project, also Jquery and PopperJS, required for this one.",
          "Git and GitHub for manage the versions of the project.",
          "Netlify is the owner of the host for this opportunity, this one works with GitHub and NPM.",
          "SCSS was utilizado like CSS PreProcessador.",
          "The app is some short for my idea, I wanted to make some bigger, but I can't for time reason"
        ]
      },
      nameApp: "WikiMovie",
      name: 'Luis Rivas'
    }
  },
  components: {
    Header, Slider, Movie
  },
  methods: {
    fetch: function(query) {
      let data = this
      axios({
        method: 'GET',
        url: `https://www.omdbapi.com/?apikey=435c3351&t=${query}`
      }).then(function (response) {
        data.movies.push(response.data)
      }).catch((err) => {
        console.log(err + ' - error in the request')
      })
    },
    fillMovies: function() {
      this.fetch('The Avengers')
      this.fetch('Age of ultron')
      this.fetch('black panther')
      this.fetch('avengers endgame')
      this.fetch('guardians of the galaxy')
      this.fetch('hulk')
      this.fetch('united')
      this.fetch('Zombies')
      this.fetch('Jurassic World')
      this.fetch('The Maze Runner')
      this.fetch('Aquaman')
      this.fetch('The Nun')
      this.fetch('Ant-Man and the Wasp')
      this.fetch('Ant-Man')
      this.fetch('homecoming')
      this.fetch('Spider-Man: Far from Home')
      this.fetch('Spider-Man: Homecoming')
      this.fetch('Deadpool')
      this.fetch('Venom')
      this.fetch('Creed')
    },
    selectMovie: function(i) {
      this.detailsMovie = this.movies[i];
      console.log(this.detailsMovie)
    }
  },
  mounted() {
    this.fillMovies()
  }
}
</script>

<style lang="scss">
@import 'css/global.scss';

.modal-header img {
  height: 400px;
}

.modal-body .list-group {
  border-radius: 0;
}
</style>
