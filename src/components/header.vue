<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark py-md-4">
  <a class="navbar-brand" href="#">{{ navTitle }}</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>
  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item" v-for="(navItem, index) in navItems" :key="index">
        <a class="nav-link" :href="navItem.href" :target="navItem._blank">{{navItem.title}}</a>
      </li>
    </ul>
    <form class="form-inline my-2 my-lg-0">
      <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
    </form>
  </div>
</nav>
</template>

<script>
export default {
  data() {
    return {
      navTitle: 'WikiMovie',
      navItems: [
        { title: 'Home', href: '#' },
        { title: 'About Us', href: '/about-us', _blank: true },
        { title: 'Contact Us', href: '/contact-us' }
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