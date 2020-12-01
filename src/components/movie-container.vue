<template>
  <div class="card">
    <div class="card-header p-0 container-header">
      <img :src="img ? img : 'https://i.imgur.com/EPDBVqq.jpg'" :alt="id + ' image'" class="img-fluid">
    </div>
    <div class="card-body">
      <p class="body-title" v-if="title">{{title}}</p>
      <p class="body-text" v-if="plot">{{plot}}</p>
      <p class="body-text" v-if="runtime"><span class="font-weight-bold">Runtime: </span> {{runtime}}</p>
      <p class="body-text" v-if="rating"><span class="font-weight-bold">Rating: </span>{{rating}}</p>
      <p class="body-text" v-if="genre"><span class="font-weight-bold">Genre: </span>{{genre}}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {

    }
  },
  props: ['img', 'title', 'id', 'plot', 'rating', 'runtime', 'genre']
}
</script>

<style>
/* General styles */
.container-header img {
  height: 425px!important;
  width: 100%;
}
</style>