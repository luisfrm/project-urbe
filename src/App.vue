<template>
  <div>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios'
axios({
  method: 'GET',
  url: 'http://www.omdbapi.com/?i=tt3896198&apikey=435c3351'
}).then(function (response) {
    console.log(response);
  })

export default {
  name: 'App',
  components: {
    
  }
}
</script>

<style lang="scss">
@import '~bootstrap/dist/css/bootstrap.min.css';
</style>
