<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark py-md-4">
  <a class="navbar-brand" href="#">{{ navTitle }}</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>
  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item" v-for="(navItem, index) in navItems" :key="index">
        <a class="nav-link" :href="navItem.href ? navItem.href : ''" :target="navItem._blank" :data-toggle="navItem.data_toggle ? navItem.data_toggle : ''" :data-target="navItem.data_target ? navItem.data_target : ''">{{navItem.title}}</a>
      </li>
    </ul>
  </div>
</nav>
</template>

<script>
export default {
  data() {
    return {
      navTitle: 'WikiMovie',
      navItems: [
        { title: 'Home', href: '/#' },
        { title: 'About Me', data_target: '#aboutme-modal', data_toggle: "modal" },
        { title: 'About It', data_target: '#aboutit-modal', data_toggle: "modal" },
        { title: 'Contact Me', data_target: '#contactme-modal', data_toggle: "modal" }
      ]
    }
  }
}
</script>

<style>
/* Desktop */
@media screen and (min-width: 981px) {
  nav.navbar {
    padding-left: 10rem;
    padding-right: 10rem;
  } 
}
</style>