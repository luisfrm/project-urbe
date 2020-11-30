<template>
  <a class="card" :href="url ? url : 'unknown'" :target="_blank ? _blank : ''">
    <div class="card-header">
      <img :src="img ? img : ''" :alt="id + ' image'">
    </div>
    <div class="card-body">
      <p v-if="title">{{title}}</p>
    </div>
  </a>
</template>

<script>
export default {
  data() {
    return {

    }
  },
  props: ['img', 'url', '_blank', 'title', 'desc', 'id']
}
</script>

<style>

</style>