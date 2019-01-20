<template>
  <header class="main-header">
    <nav class="main-nav">
      <ul class="nav-links">
        <!-- instead wrapping nut-link in li element we can do something like this -->
        <!-- in the end vue will transform this in to li > a proper elements -->
        <nuxt-link to="/" tag="li"><a>All posts</a></nuxt-link>
        <nuxt-link to="/about" tag="li"><a>About</a></nuxt-link>
      </ul>
    </nav>
  </header>
</template>

<style scoped>
.main-header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background: #022d30;
}
</style>

