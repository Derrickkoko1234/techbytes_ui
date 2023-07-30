<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>
<!-- <RouterLink to="/about">About</RouterLink> -->
<template>
  <header>
    <router-link :to="`/`" class="news-link">
    <h1>TechBytes</h1>
    </router-link>
  </header>

  <RouterView />
</template>

<style>
nav {
  background-color: #333;
  color: #fff;
  padding: 10px;
}

nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
}

nav li {
  margin-right: 20px;
}

nav a {
  text-decoration: none;
  color: #fff;
  padding: 5px;
}

.logo {
  font-size: 24px;
  font-weight: bold;
  margin-right: 20px;
}

.news-link {
  color: #fff;
}
</style>
